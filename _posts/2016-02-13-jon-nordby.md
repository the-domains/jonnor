---
inFeed: true
hasPage: false
inNav: false
isBasedOnUrl: 'http://www.jonnor.com/2011/08/combining-pyside-and-pygobject-introspection-bindings/'
inLanguage: en
starred: false
keywords:
  - geglnode
  - gegl
  - pyobj
  - geglnodeptr
  - pygobject
  - pyobject
  - gobject
  - inline
  - python
  - static
description: ''
datePublished: '2016-02-13T20:35:24.887Z'
dateModified: '2016-02-13T19:46:53.144Z'
author: []
related: []
app_links: []
title: Combining PySide and PyGObject introspection bindings
sourcePath: _posts/2016-02-13-jon-nordby.md
published: true
authors: []
publisher:
  name: Jonnor
  domain: www.jonnor.com
  url: 'http://www.jonnor.com'
  favicon: null
_context: 'http://schema.org'
_type: Article

---
# Combining PySide and PyGObject introspection bindings

Some while back I added basic GObject Introspection support to [GEGL][0] and GEGL-GTK master a while back. This will\* allow application developers to write their Gegl + Gtk based applications in any language supported by [GObject Introspection][1], like Python, Vala and Javascript. For GeglQt, the [Qt][2] integration library for using Gegl in Qt based applications, it was natural to use [PySide][3] to provide Python bindings for it. The initial setup was quick and easy, thanks to the [binding tutorial][4], but there was one challenge.

The current widgets provided by GeglQt are for displaying the output of a node in the GEGL graph. Therefore they have methods with the following signature to hook up it up:

    [From gegl-qt/nodeviewwidget.h][5] GeglNode *inputNode() const; void setInputNode(GeglNode *node);

_GeglNode_ is a _GObject_ (from the C based [glib][6]) subclass, and without help the bindings generator (Shiboken) does not know what to do with it so the method cannot be bound. PySide could have been used to also generate bindings for Gegl itself, but what we actually want to do is to make use of the existing PyGObject based bindings.

[Marcelo Lira][7] on \#pyside let me know that this should be possible by adding some annotations to the typesystem.xml file, and implementing a Shiboken::Converter. It is indeed possible, and for the above type looks something like this:

    [From typesystem_gegl-qt.xml][8] <primitive-type name="GeglNodePtr"> <conversion-rule file="geglnode_conversions.h"/> <include file-name="pygobject.h" location="global"/> </primitive-type> 

    [From geglnode_conversions.h][9] namespace Shiboken { template<> struct Converter<GeglNodePtr> { static inline bool checkType(PyObject* pyObj) { return GEGL_IS_NODE(((PyGObject *)pyObj)->obj); } static inline bool isConvertible(PyObject* pyObj) { return GEGL_IS_NODE(((PyGObject *)pyObj)->obj); } static inline PyObject* toPython(void* cppObj) { return pygobject_new(G_OBJECT((cppObj))); } static inline PyObject* toPython(const GeglNodePtr geglNode) { return pygobject_new(G_OBJECT(geglNode)); } static inline GeglNodePtr toCpp(PyObject* pyObj) { return GEGL_NODE(((PyGObject *)pyObj)->obj); } }; }

The PyGObject C API and the GObject type system is here being used to implement what Shiboken needs. The attentive reader will note that _GeglNodePtr_ is used and not _GeglNode\*_. This is a simple " _typedef GeglNode \* GeglNodePtr_ ", which looks to be neccesary with current PySide (1.0.6) to avoid it being confused by the pointer. Hopefully that is fixable and won't be necessary in the future.

With this solved, I committed the [initial Python support][10] to GeglQt master yesterday. It contains a [trivial Python example][11] showing the usage. Some build cleanups, binding generator tweaks and testing remains to be done, but expect Python support to be a prominent feature for GeglQt 0.1.0

\* There are still a lot of GObject Introspection annotations missing in Gegl. See the [tracking bug][12]. Help wanted!
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][13]

[0]: http://www.gegl.org/
[1]: https://live.gnome.org/GObjectIntrospection
[2]: http://qt.nokia.com/
[3]: http://www.pyside.org/
[4]: http://developer.qt.nokia.com/wiki/PySide_Binding_Generation_Tutorial
[5]: http://git.gnome.org/browse/gegl-qt/tree/gegl-qt/nodeviewwidget.h
[6]: http://developer.gnome.org/glib/
[7]: http://setanta.wordpress.com/
[8]: http://git.gnome.org/browse/gegl-qt/tree/pygegl-qt/typesystem_gegl-qt.xml
[9]: http://git.gnome.org/browse/gegl-qt/tree/pygegl-qt/geglnode_conversions.h
[10]: http://git.gnome.org/browse/gegl-qt/commit/?id=1a444f65ff80bb15bd43ea1a0206345b83c665e6
[11]: http://git.gnome.org/browse/gegl-qt/tree/examples/pyside-basic.py
[12]: https://bugzilla.gnome.org/show_bug.cgi?id=645822
[13]: http://www.jonnor.com/wp/?flattrss_redirect&id=453&md5=e9ce019de8f99aa917a8af716dfc8639