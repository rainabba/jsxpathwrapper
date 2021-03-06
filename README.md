# Xpath Wrapper

[![Build Status](https://travis-ci.org/dimensional-de/jsxpathwrapper.svg?branch=master)](https://travis-ci.org/dimensional-de/jsxpathwrapper)

Simplify the XPath handling for JavaScript. If you're using XPath
in JavaScript you have to keep track of three variables. The document, the context
and the namespace resolver.

This library combines the three into one object.

Basic Usage:

```javascript
var xpath = new XpathWrapper(
  source,  {atom : 'http://www.w3.org/2005/Atom'}
);
xpath.evaluate('//atom:entry').each(
  function(entry, index) {
    console.log(
      xpath.evaluate('string(atom:title)', entry)
    }
  }
}
```

## Constructor

The `source` argument can be an XML string, a document or a node. If it
is a node it will be set as default context, too - otherwise the document.

The second argument is a list of namespaces or a function that resolves the
namespace prefixes you're using in your XPath expressions.

## evaluate()

The first argument is the XPath expression and mandatory. The second argument
is the optional context for the expression. The wrapper has
a default context depending on the constructor.

The third argument is an `XpathResult.*_TYPE` constant. It forces a specific
result type. If not provided then `XpathResult.ANY_TYPE` is used.

The return value of evaluate() depends on the actual XpathResult. If it
is a scalar type the scalar value will be returned. If it is a list of nodes
a `XpathNodes` object is returned.

You can force the return of a single node using `XPathResult.FIRST_ORDERED_NODE_TYPE`.

## XpathNodes

An internal object type returned for node lists.

### XpathNodes.toArray()

Converts the nodes list into an array and returns it.

### XpathNodes.each()

Calls the provided callback for each node.

## IE Support

Most Modern Browsers have native support for DOM3 Xpath - Internet Explorer has not.
The wrapper can use [Cameron McCormack xpath.js](http://mcc.id.au/xpathjs) library for that.



