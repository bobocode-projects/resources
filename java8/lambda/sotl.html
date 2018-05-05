<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns='http://www.w3.org/1999/xhtml'>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ascii"/>
    <title>State of the Lambda</title>
    <link rel="shortcut icon" href="http://openjdk.java.net/images/nanoduke.ico"/>
    <style type="text/css">

      A { text-decoration: none; }
      A:link, A:visited { color: #437291; }
      A:visited { color: #666666; }
      A[href]:hover { color: #e76f00; }
      A IMG { border-width: 0px; }
      IMG { background: white; }
      A.internal { color: #b00; }
      A[name] { color: black; }

      BODY {
        background: white;
        margin: 2em;
        font-size: medium;
        width: 60em;
        margin-bottom: 100%;
      }
      BODY { font-family: Bitstream Vera Sans, Verdana, sans serif; }
      PRE { font-family: monospace; }
      CODE { font-family: courier new, monospace; font-size: medium; font-weight: bold; }

      P { margin: 1ex 0em; }
      PRE { margin: 1.5ex 2em; }
      BLOCKQUOTE { margin: 1.5ex 2em; }
      LI BLOCKQUOTE { margin-left: 0em; }
      LI { margin: 0ex 0em; }
      .todo { color: darkred; text-align: right; }

      TABLE { border-collapse: collapse; padding: 0px; }
      TD { padding: 0px; vertical-align: top; }

      UL LI { list-style-type: square; }

      DIV.summary { margin: 2ex 2em; }

      DIV.head { margin-bottom: 2em; }
      DIV.doctitle { font-size: x-large; font-weight: bold; }
      DIV.twarn { color: #cc0000; font-size: smaller; font-weight: bold;
                  margin-bottom: 1.5ex; }
      DIV.authors { margin-top: 1ex; font-size: large; }
      DIV.author A { font-style: italic; }
      DIV.version { font-size: medium; margin-top: 1ex; }
      DIV.copyright, DIV.comments { font-size: small; }
      DIV.version SPAN.modified { color: green; font-weight: bold; }
      DIV.head DIV.notes { margin-top: 1ex; }

      P.subsection { margin-top: 2ex; }
      P.subsection:first-child { margin-top: 1ex; }
      P SPAN.title { font-weight: bold; padding-right: 1em; }

      HR { border: 0px; border-top: 1px solid black; margin: 2ex 0em; }

      DIV.qa { margin-top: 2ex; }

      H1 { font-size: x-large; }
      H2 { font-size: large; margin-top: 3ex; margin-bottom: 0ex; }

      PRE {
        padding: 1px 1ex;
        background: #e8e8e8;
        font-size: smaller;
        ZZdisplay: none;
      }

    </style>
  </head>
  <body>
<h1>State of the Lambda</h1>

<!-- This document is in Markdown format:
     http://daringfireball.net/projects/markdown/
 -->

<h4>September 2013</h4>

<h4>Java SE 8 Edition</h4>

<p>This is an informal overview of the enhancements to the Java
programming language specified by <a href="http://jcp.org/en/jsr/detail?id=335">JSR 335</a> and implemented in the
OpenJDK <a href="http://openjdk.java.net/projects/lambda/">Lambda Project</a>.  It refines the <a href="http://cr.openjdk.java.net/~briangoetz/lambda/lambda-state-4.html">previous
iteration</a> posted in December 2011.  A formal description of
some of the language changes may be found in the 
<a href="http://jcp.org/aboutJava/communityprocess/edr/jsr335/index.html">Early Draft Specification</a> for the JSR; an OpenJDK <a href="http://jdk8.java.net/lambda/">Developer Preview</a> 
is also
available.  Additional historical design documents can be found at the
<a href="http://openjdk.java.net/projects/lambda/">OpenJDK project page</a>.  There is also a companion
document, <a href="http://cr.openjdk.java.net/~briangoetz/lambda/lambda-libraries-final.html">State of the Lambda, Libraries Edition</a>, describing 
the library enhancements added as part of JSR 335.  </p>

<p>The high-level goal of Project Lambda is to enable programming patterns
that require modeling code as data to be convenient and idiomatic in
Java.  The principal new language features include:</p>

<ul>
<li>Lambda expressions (informally, "closures" or "anonymous methods")</li>
<li>Method and constructor references</li>
<li>Expanded target typing and type inference</li>
<li>Default and static methods in interfaces</li>
</ul>

<p>These are described and illustrated below.</p>

<h2>1.  Background</h2>

<p>Java is, primarily, an object-oriented programming language.  In both
object-oriented and functional languages, basic values can dynamically
encapsulate program behavior: object-oriented languages have objects
with methods, and functional languages have functions.  This
similarity may not be obvious, however, because Java objects tend to
be relatively heavyweight: instantiations of separately-declared
classes wrapping a handful of fields and many methods.</p>

<p>Yet it is common for some objects to essentially encode nothing more
than a function.  In a typical use case, a Java API defines an
interface, sometimes described as a "callback interface," expecting
the user to provide an instance of the interface when invoking the
API.  For example:</p>

<pre><code>public interface ActionListener { 
    void actionPerformed(ActionEvent e);
}
</code></pre>

<p>Rather than declaring a class that implements <code>ActionListener</code> for the
sole purpose of allocating it once at an invocation site, a user
typically instantiates the implementing class inline, anonymously:</p>

<pre><code>button.addActionListener(new ActionListener() { 
  public void actionPerformed(ActionEvent e) { 
    ui.dazzle(e.getModifiers());
  }
});
</code></pre>

<p>Many useful libraries rely on this pattern.  It is particularly
important for parallel APIs, in which the code to execute must be
expressed independently of the thread in which it will run.  The
parallel-programming domain is of special interest, because as Moore's
Law continues to give us more cores but not faster cores, serial APIs
are limited to a shrinking fraction of available processing power.</p>

<p>Given the increasing relevance of callbacks and other functional-style
idioms, it is important that modeling code as data in Java be as
lightweight as possible.  In this respect, anonymous inner classes are
imperfect for a <a href="http://blogs.oracle.com/jrose/entry/better_closures">number of reasons</a>, primarily:</p>

<ol>
<li>Bulky syntax</li>
<li>Confusion surrounding the meaning of names and <code>this</code></li>
<li>Inflexible class-loading and instance-creation semantics</li>
<li>Inability to capture non-final local variables</li>
<li>Inability to abstract over control flow</li>
</ol>

<p>This project addresses many of these issues. It eliminates (1) and (2) by
introducing new, much more concise expression forms with local scoping
rules, sidesteps (3) by defining the semantics of the new expressions in
a more flexible, optimization-friendly manner, and ameliorates (4) by
allowing the compiler to infer finality (allowing capture of
<em>effectively final</em> local variables).</p>

<p>However, it is <em>not</em> a goal of this project to address all the
problems of inner classes.  Neither arbitrary capture of mutable
variables (4) nor nonlocal control flow (5) are within this project's
scope (though such features may be revisited in a future iteration of
the language.)  </p>

<h2>2.  Functional interfaces</h2>

<p>The anonymous inner class approach, despite its limitations, has the
nice property of fitting very cleanly into Java's type system: a
function value with an interface type.  This is convenient for a
number of reasons: interfaces are already an intrinsic part of the
type system; they naturally have a runtime representation; and they
carry with them informal contracts expressed by Javadoc comments, such
as an assertion that an operation is commutative.</p>

<p>The interface <code>ActionListener</code>, used above, has just one method. Many
common callback interfaces have this property, such as <code>Runnable</code> and
<code>Comparator</code>. We'll give all interfaces that have just one method a
name: <em>functional interfaces</em>.  (These were previously called
<em>SAM Types</em>, which stood for "Single Abstract Method".)</p>

<p>Nothing special needs to be done to declare an interface as
functional; the compiler identifies it as such based on its structure.
(This identification process is a little more than just counting
method declarations; an interface might redundantly declare a method
that is automatically provided by the class <code>Object</code>, such as
<code>toString()</code>, or might declare static or default methods, none of
which count against the one-method limit.)  However, API authors may
additionally capture the <em>design intent</em> that an interface be
functional (as opposed to accidentally having only one method) with
the <code>@FunctionalInterface</code> annotation, in which case the compiler will
validate that the interface meets the structural requirements to be a
functional interface.</p>

<p>An alternative (or complementary) approach to function types,
suggested by some early proposals, would have been to introduce a new,
<em>structural</em> function type, sometimes called <em>arrow types</em>.  A type
like "function from a <code>String</code> and an <code>Object</code> to an <code>int</code>" might be
expressed as <code>(String,Object)-&gt;int</code>.  This idea was considered and
rejected, at least for now, due to several disadvantages:</p>

<ul>
<li>It would add complexity to the type system and further mix structural
and nominal types (Java is almost entirely nominally typed).</li>
<li>It would lead to a divergence of library styles -- some
libraries would continue to use callback interfaces, while others
would use structural function types.</li>
<li>The syntax could be unwieldy, especially when checked exceptions were
included.</li>
<li>It is unlikely that there would be a runtime representation for
each distinct function type, meaning developers would be further
exposed to and limited by erasure. For example, it would not be
possible (perhaps surprisingly) to overload methods <code>m(T-&gt;U)</code> and
<code>m(X-&gt;Y)</code>.</li>
</ul>

<p>So, we have instead followed the path of "use what you
know" -- since existing libraries use functional interfaces
extensively, we codify and leverage this pattern.  This enables
<em>existing</em> libraries to be used with lambda expressions.  </p>

<p>To illustrate, here is a sampling of some of the functional interfaces
already in Java SE 7 that are well-suited for being used with the new
language features; the examples that follow illustrate the use of a
few of them.</p>

<ul>
<li><a href="http://download.oracle.com/javase/7/docs/api/java/lang/Runnable.html"><code>java.lang.Runnable</code></a></li>
<li><a href="http://download.oracle.com/javase/7/docs/api/java/util/concurrent/Callable.html"><code>java.util.concurrent.Callable</code></a></li>
<li><a href="http://download.oracle.com/javase/7/docs/api/java/security/PrivilegedAction.html"><code>java.security.PrivilegedAction</code></a></li>
<li><a href="http://download.oracle.com/javase/7/docs/api/java/util/Comparator.html"><code>java.util.Comparator</code></a></li>
<li><a href="http://download.oracle.com/javase/7/docs/api/java/io/FileFilter.html"><code>java.io.FileFilter</code></a></li>
<li><a href="http://www.fxfrog.com/docs_www/api/java/beans/PropertyChangeListener.html"><code>java.beans.PropertyChangeListener</code></a></li>
</ul>

<p>In addition, Java SE 8 adds a new package,
<a href="http://download.java.net/jdk8/docs/api/java/util/function/package-summary.html"><code>java.util.function</code></a>, which contains functional
interfaces that are expected to be commonly used, such as:</p>

<ul>
<li><code>Predicate&lt;T&gt;</code> -- a boolean-valued property of an object </li>
<li><code>Consumer&lt;T&gt;</code> -- an action to be performed on an object</li>
<li><code>Function&lt;T,R&gt;</code> -- a function transforming a T to a R</li>
<li><code>Supplier&lt;T&gt;</code> -- provide an instance of a T (such as a factory)</li>
<li><code>UnaryOperator&lt;T&gt;</code> -- a function from T to T</li>
<li><code>BinaryOperator&lt;T&gt;</code> -- a function from (T, T) to T</li>
</ul>

<p>In addition to these basic "shapes", there are also primitive
specializations such as <code>IntSupplier</code> or <code>LongBinaryOperator</code>.
(Rather than provide the full complement of primitive specializations,
we provide only specializations for <code>int</code>, <code>long</code>, and <code>double</code>;
the other primitive types can be accomodated through conversions.)
Similarly, there are some specializations for multiple arities, such
as <code>BiFunction&lt;T,U,R&gt;</code>, which represents a function from <code>(T,U)</code> to
<code>R</code>.  </p>

<h2>3.  Lambda expressions</h2>

<p>The biggest pain point for anonymous classes is bulkiness.  They have
what we might call a "vertical problem": the <code>ActionListener</code> instance
from section 1 uses five lines of source code to encapsulate a single
aspect of behavior.</p>

<p>Lambda expressions are anonymous methods, aimed at addressing the
"vertical problem" by replacing the machinery of anonymous inner
classes with a lighter-weight mechanism.</p>

<p>Here are some examples of lambda expressions:</p>

<pre><code>(int x, int y) -&gt; x + y

() -&gt; 42

(String s) -&gt; { System.out.println(s); }
</code></pre>

<p>The first expression takes two integer arguments, named <code>x</code> and <code>y</code>,
and returns their sum.  The second takes <em>no</em> arguments and returns
the integer <code>42</code>.  The third takes a string and prints it to the
console, returning nothing.</p>

<p>The general syntax consists of an argument list, the arrow token <code>-&gt;</code>,
and a body.  The body can either be a single expression, or a statement
block.  In the expression form, the body is simply evaluated and
returned.  In the block form, the body is evaluated like a method
body -- a <code>return</code> statement returns control to the caller of the
anonymous method; <code>break</code> and <code>continue</code> are illegal at the top level,
but are of course permitted within loops; and if the body produces a
result, every control path must return something or throw an exception.</p>

<p>The syntax is optimized for the common case in which a lambda
expression is quite small, as illustrated above. For example, the
expression-body form eliminates the need for a <code>return</code> keyword, which
could otherwise represent a substantial syntactic overhead relative to
the size of the expression.</p>

<p>It is also expected that lambda expressions will frequently appear in
nested contexts, such as the argument to a method invocation or the
result of <em>another</em> lambda expression. To minimize noise in these cases,
unnecessary delimiters are avoided.  However, for situations in which
it is useful to set the entire expression apart, it can be surrounded
with parentheses, just like any other expression.</p>

<p>Here are some examples of lambda expressions appearing in statements:</p>

<pre><code>FileFilter java = (File f) -&gt; f.getName().endsWith(".java");

String user = doPrivileged(() -&gt; System.getProperty("user.name"));

new Thread(() -&gt; {
  connectToService();
  sendNotification();
}).start();
</code></pre>

<h2>4.  Target typing</h2>

<p>Note that the name of a functional interface is <em>not</em> part of the lambda
expression syntax.  So what kind of object does a lambda expression
represent?  Its type is inferred from the surrounding context.  For
example, the following lambda expression is an <code>ActionListener</code>:</p>

<pre><code>ActionListener l = (ActionEvent e) -&gt; ui.dazzle(e.getModifiers());
</code></pre>

<p>An implication of this approach is that the same lambda expression can
have different types in different contexts:</p>

<pre><code>Callable&lt;String&gt; c = () -&gt; "done";

PrivilegedAction&lt;String&gt; a = () -&gt; "done";
</code></pre>

<p>In the first case, the lambda expression <code>() -&gt; "done"</code> represents an
instance of <code>Callable</code>.  In the second case, the same expression
represents an instance of <code>PrivilegedAction</code>.</p>

<p>The compiler is responsible for inferring the type of each lambda
expression. It uses the type expected in the context in which the
expression appears; this type is called the <em>target type</em>.  A lambda
expression can only appear in a context whose target type is a
functional interface.</p>

<p>Of course, no lambda expression will be compatible with <em>every</em>
possible target type.  The compiler checks that the types used by the
lambda expression are consistent with the target type's method
signature. That is, a lambda expression can be assigned to a target
type <code>T</code> if all of the following conditions hold:</p>

<ul>
<li><code>T</code> is a functional interface type</li>
<li>The lambda expression has the same number of parameters as <code>T</code>'s
method, and those parameters' types are the same</li>
<li>Each expression returned by the lambda body is compatible with <code>T</code>'s
method's return type</li>
<li>Each exception thrown by the lambda body is allowed by <code>T</code>'s method's
<code>throws</code> clause</li>
</ul>

<p>Since a functional interface target type already "knows" what types
the lambda expression's formal parameters should have, it is often
unnecessary to repeat them.  The use of target typing enables
the lambda parameters' types to be inferred:</p>

<pre><code>Comparator&lt;String&gt; c = (s1, s2) -&gt; s1.compareToIgnoreCase(s2);
</code></pre>

<p>Here, the compiler infers that the type of <code>s1</code> and <code>s2</code> is <code>String</code>.
In addition, when there is just one parameter whose type is inferred
(a very common case), the parentheses surrounding a single parameter
name are optional:</p>

<pre><code>FileFilter java = f -&gt; f.getName().endsWith(".java");

button.addActionListener(e -&gt; ui.dazzle(e.getModifiers()));
</code></pre>

<p>These enhancements further a desirable design goal: "Don't turn a
vertical problem into a horizontal problem."  We want the reader of the
code to have to wade through as little syntax as possible before
arriving at the "meat" of the lambda expression.</p>

<p>Lambda expressions are not the first Java expressions to have
context-dependent types: generic method invocations and "diamond"
constructor invocations, for example, are similarly type-checked based
on an assignment's target type.</p>

<pre><code>List&lt;String&gt; ls = Collections.emptyList();
List&lt;Integer&gt; li = Collections.emptyList();

Map&lt;String,Integer&gt; m1 = new HashMap&lt;&gt;();
Map&lt;Integer,String&gt; m2 = new HashMap&lt;&gt;();
</code></pre>

<h2>5.  Contexts for target typing</h2>

<p>We stated earlier that lambda expressions can only appear in contexts
that have target types.  The following contexts have target types:</p>

<ul>
<li>Variable declarations</li>
<li>Assignments</li>
<li>Return statements</li>
<li>Array initializers</li>
<li>Method or constructor arguments</li>
<li>Lambda expression bodies</li>
<li>Conditional expressions (<code>?:</code>)</li>
<li>Cast expressions</li>
</ul>

<p>In the first three cases, the target type is simply the type being
assigned to or returned.</p>

<pre><code>Comparator&lt;String&gt; c;
c = (String s1, String s2) -&gt; s1.compareToIgnoreCase(s2);

public Runnable toDoLater() {
  return () -&gt; {
    System.out.println("later");
  };
}
</code></pre>

<p>Array initializer contexts are like assignments, except that the
"variable" is an array component and its type is derived from the
array's type.</p>

<pre><code>filterFiles(new FileFilter[] { 
               f -&gt; f.exists(), f -&gt; f.canRead(), f -&gt; f.getName().startsWith("q") 
            });
</code></pre>

<p>In the method argument case, things are more complicated: target type
determination interacts with two other language features, <em>overload
resolution</em> and <em>type argument inference</em>.</p>

<p>Overload resolution involves finding the best method declaration for a
particular method invocation.  Since different declarations have
different signatures, this can impact the target type of a lambda
expression used as an argument.  The compiler will use what it knows
about the lambda expression to make this choice.  If a lambda
expression is <em>explicitly typed</em> (specifies the types of its
parameters), the compiler will know not only the parameter types but
also the type of all return expressions in its body.  If the lambda is
<em>implicitly typed</em> (inferred parameter types), overload resolution
will ignore the lambda body and only use the number of lambda
parameters.</p>

<p>If the choice of a best method declaration is ambiguous, casts or
explicit lambdas can provide additional type information for the
compiler to disambiguate.  If the return type targeted by a lambda
expression depends on type argument inference, then the lambda body
may provide information to the compiler to help infer the type
arguments.</p>

<pre><code>List&lt;Person&gt; ps = ...
String&lt;String&gt; names = ps.stream().map(p -&gt; p.getName());
</code></pre>

<p>Here, <code>ps</code> is a <code>List&lt;Person&gt;</code>, so <code>ps.stream()</code> is a
<code>Stream&lt;Person&gt;</code>.  The <code>map()</code> method is generic in <code>R</code>, where the
parameter of <code>map()</code> is a <code>Function&lt;T,R&gt;</code>, where <code>T</code> is the stream
element type.  (<code>T</code> is known to be <code>Person</code> at this point.)  Once the
overload is selected and the lambda's target type is known, we need to
infer <code>R</code>; we do this by type-checking the lambda body, and
discovering that its return type is <code>String</code>, and hence <code>R</code> is
<code>String</code>, and therefore the <code>map()</code> expression has a type of
<code>Stream&lt;String&gt;</code>.  Most of the time, the compiler just figures this
all out, but if it gets stuck, we can provide additional type
information via an explicit lambda (give the argument <code>p</code> an explicit
type), casting the lambda to an explicit target type such as
<code>Function&lt;Person,String&gt;</code>, or providing an explicit type witness for
the generic parameter <code>R</code> (<code>.&lt;String&gt;map(p -&gt; p.getName())</code>).</p>

<p>Lambda expressions themselves provide target types for their bodies,
in this case by deriving that type from the outer target type. This
makes it convenient to write functions that return other functions:</p>

<pre><code>Supplier&lt;Runnable&gt; c = () -&gt; () -&gt; { System.out.println("hi"); };
</code></pre>

<p>Similarly, conditional expressions can "pass down" a target type
from the surrounding context:</p>

<pre><code>Callable&lt;Integer&gt; c = flag ? (() -&gt; 23) : (() -&gt; 42);
</code></pre>

<p>Finally, cast expressions provide a mechanism to explicitly provide
a lambda expression's type if none can be conveniently inferred
from context:</p>

<pre><code>// Illegal: Object o = () -&gt; { System.out.println("hi"); };
Object o = (Runnable) () -&gt; { System.out.println("hi"); };
</code></pre>

<p>Casts are also useful to help resolve ambiguity when a method
declaration is overloaded with unrelated functional interface types.</p>

<p>The expanded role of target typing in the compiler is not limited to
lambda expressions: generic method invocations and "diamond" constructor
invocations can also take advantage of target types wherever they are
available.  The following declarations are illegal in Java SE 7 but
valid in Java SE 8:</p>

<pre><code>List&lt;String&gt; ls =
  Collections.checkedList(new ArrayList&lt;&gt;(), String.class);

Set&lt;Integer&gt; si = flag ? Collections.singleton(23)
                       : Collections.emptySet();
</code></pre>

<h2>6.  Lexical scoping</h2>

<p>Determining the meaning of names (and <code>this</code>) in inner classes is
significantly more difficult and error-prone than when classes are
limited to the top level.  Inherited members -- including methods of
class <code>Object</code> -- can accidentally shadow outer declarations, and
unqualified references to <code>this</code> always refer to the inner class itself.</p>

<p>Lambda expressions are much simpler: they do not inherit any names from
a supertype, nor do they introduce a new level of scoping.  Instead,
they are lexically scoped, meaning names in the body are interpreted
just as they are in the enclosing environment (with the addition of new
names for the lambda expression's formal parameters).  As a natural
extension, the <code>this</code> keyword and references to its members have the
same meaning as they would immediately outside the lambda expression.</p>

<p>To illustrate, the following program prints <code>"Hello, world!"</code> twice to
the console:</p>

<pre><code>public class Hello {
  Runnable r1 = () -&gt; { System.out.println(this); }
  Runnable r2 = () -&gt; { System.out.println(toString()); }

  public String toString() { return "Hello, world!"; }

  public static void main(String... args) {
    new Hello().r1.run();
    new Hello().r2.run();
  }
}
</code></pre>

<p>The equivalent using anonymous inner classes would instead, perhaps to
the programmer's surprise, print something like <code>Hello$1@5b89a773</code> and
<code>Hello$2@537a7706</code>.</p>

<p>Consistent with the lexical-scoping approach, and following the pattern
set by other local parameterized constructs like <code>for</code> loops and <code>catch</code>
clauses, the parameters of a lambda expression must not shadow any local
variables in the enclosing context.</p>

<h2>7.  Variable capture</h2>

<p>The compiler check for references to local variables of enclosing
contexts in inner classes (<em>captured</em> variables) is quite restrictive in
Java SE 7: an error occurs if the captured variable is not declared
<code>final</code>.  We relax this restriction -- for both lambda
expressions and inner classes -- by also allowing the capture of
<em>effectively final</em> local variables.</p>

<p>Informally, a local variable is effectively final if its initial value
is never changed -- in other words, declaring it <code>final</code> would not cause
a compilation failure.</p>

<pre><code>Callable&lt;String&gt; helloCallable(String name) {
  String hello = "Hello";
  return () -&gt; (hello + ", " + name);
}
</code></pre>

<p>References to <code>this</code> -- including implicit references through
unqualified field references or method invocations -- are,
essentially, references to a <code>final</code> local variable.  Lambda bodies that
contain such references capture the appropriate instance of <code>this</code>.  In
other cases, no reference to <code>this</code> is retained by the object.</p>

<p>This has a beneficial implication for memory management: while inner
class instances always hold a strong reference to their enclosing
instance, lambdas that do not capture members from the enclosing
instance do <em>not</em> hold a reference to it.  This characteristic of inner
class instances can often be a source of memory leaks.</p>

<p>While we relax the syntactic restrictions on captured values, we still
prohibit capture of mutable local variables.  The reason is that
idioms like this:</p>

<pre><code>int sum = 0;
list.forEach(e -&gt; { sum += e.size(); }); // ERROR
</code></pre>

<p>are fundamentally serial; it is quite difficult to write lambda bodies
like this that do not have race conditions.  Unless
we are willing to enforce -- preferably at compile time -- that
such a function cannot escape its capturing thread, this feature may
well cause more trouble than it solves.  Lambda expressions close over
<em>values</em>, not <em>variables</em>.  </p>

<p>Another reason to not support capture of mutable variables is that
there's a better way to address accumulation problems without
mutation, and instead treat this problem as a <em>reduction</em>.  The
<a href="http://download.java.net/jdk8/docs/api/java/util/stream/package-summary.html"><code>java.util.stream</code></a> package provides both general and
specialized (such as sum, min, and max) reductions on collections and
other data structures.  For example, instead of using <code>forEach</code> and
mutation, we could do a reduction which is safe both sequentially or
in parallel:</p>

<pre><code>int sum = list.stream()
              .mapToInt(e -&gt; e.size())
              .sum();
</code></pre>

<p>The <code>sum()</code> method is provided for convenience, but is equivalent to the
more general form of reduction:</p>

<pre><code>int sum = list.stream()
              .mapToInt(e -&gt; e.size())
              .reduce(0, (x,y) -&gt; x+y);
</code></pre>

<p>Reduction takes a base value (in case the input is empty) and an
operator (here, addition), and computes the following expression:</p>

<pre><code>0 + list[0] + list[1] + list[2] + ...
</code></pre>

<p>Reduction can be done with other operations as well, such as minimum,
maximum, product, etc, and if the operator is associative, is easily
and safely parallelized.  So, rather than supporting an idiom that is
fundamentally sequential and prone to data races (mutable
accumulators), we instead choose to provide library support to express
accumulations in a more parallelizable and less error-prone way.  </p>

<h2>8.  Method references</h2>

<p>Lambda expressions allow us to define an anonymous method and treat
it as an instance of a functional interface.  It is often desirable to
do the same with an <em>existing</em> method.</p>

<p>Method references are expressions which have the same treatment as
lambda expressions (i.e., they require a target type and encode
functional interface instances), but instead of providing a method body,
they refer an existing method by name.</p>

<p>For example, consider a <code>Person</code> class that can be sorted by name or by
age.  </p>

<pre><code>class Person { 
    private final String name;
    private final int age;

    public int getAge() { return age; }
    public String getName() { return name; }
   ...
}

Person[] people = ...
Comparator&lt;Person&gt; byName = Comparator.comparing(p -&gt; p.getName());
Arrays.sort(people, byName);
</code></pre>

<p>We can rewrite this to use a method reference to <code>Person.getName()</code>
instead:</p>

<pre><code>Comparator&lt;Person&gt; byName = Comparator.comparing(Person::getName);
</code></pre>

<p>Here, the expression <code>Person::getName</code> can be considered shorthand for
a lambda expression which simply invokes the named method with its
arguments, and returns the result.  While the method reference may not
(in this case) be any more syntactically compact, it is clearer -- the
method that we want to call has a name, and so we can refer to it
directly by name.</p>

<p>Because the functional interface method's parameter types act as
arguments in an implicit method invocation, the referenced method
signature is allowed to manipulate the parameters -- via widening,
boxing, grouping as a variable-arity array, etc. -- just like a
method invocation.</p>

<pre><code>Consumer&lt;Integer&gt; b1 = System::exit;   // void exit(int status)
Consumer&lt;String[]&gt; b2 = Arrays::sort;  // void sort(Object[] a)
Consumer&lt;String&gt; b3 = MyProgram::main; // void main(String... args)
Runnable r = MyProgram::main;          // void main(String... args)
</code></pre>

<h2>9.  Kinds of method references</h2>

<p>There are several different kinds of method references, each
with slightly different syntax:</p>

<ul>
<li>A static method (<code>ClassName::methName</code>)</li>
<li>An instance method of a particular object (<code>instanceRef::methName</code>)</li>
<li>A <code>super</code> method of a particular object (<code>super::methName</code>)</li>
<li>An instance method of an arbitrary object of a particular type (<code>ClassName::methName</code>)</li>
<li>A class constructor reference (<code>ClassName::new</code>)</li>
<li>An array constructor reference (<code>TypeName[]::new</code>)</li>
</ul>

<p>For a static method reference, the class to which the method belongs
precedes the <code>::</code> delimiter, such as in <code>Integer::sum</code>.</p>

<p>For a reference to an instance method of a particular object, an
expression evaluating to an object reference precedes the delimiter:</p>

<pre><code>Set&lt;String&gt; knownNames = ...
Predicate&lt;String&gt; isKnown = knownNames::contains;
</code></pre>

<p>Here, the implicit lambda expression would capture the <code>String</code> object
referred to by <code>knownNames</code>, and the body would invoke <code>Set.contains</code>
using that object as the receiver.</p>

<p>The ability to reference the method of a specific object provides a
convenient way to convert between different functional interface types:</p>

<pre><code>Callable&lt;Path&gt; c = ...
PrivilegedAction&lt;Path&gt; a = c::call;
</code></pre>

<p>For a reference to an instance method of an arbitrary object, the type
to which the method belongs precedes the delimiter, and the invocation's
receiver is the first parameter of the functional interface method:</p>

<pre><code>Function&lt;String, String&gt; upperfier = String::toUpperCase;
</code></pre>

<p>Here, the implicit lambda expression has one parameter, the string to
be converted to upper case, which becomes the receiver of the
invocation of the <code>toUpperCase()</code> method.</p>

<p>If the class of the instance method is generic, its type parameters can
be provided before the <code>::</code> delimiter or, in most cases, inferred from
the target type.</p>

<p>Note that the syntax for a static method reference might also be
interpreted as a reference to an instance method of a class. The
compiler determines which is intended by attempting to identify an
applicable method of each kind (noting that the instance method has one
less argument).</p>

<p>For all forms of method references, method type arguments are inferred
as necessary, or they can be explicitly provided following the <code>::</code>
delimiter.</p>

<p>Constructors can be referenced in much the same was as static methods by
using the name <code>new</code>:</p>

<pre><code>SocketImplFactory factory = MySocketImpl::new;
</code></pre>

<p>If a class has multiple constructors, the target type's method signature
is used to select the best match in the same way that a constructor
invocation is resolved.</p>

<p>For inner classes, no syntax supports explicitly providing an
enclosing instance parameter at the site of the constructor reference.</p>

<p>If the class to instantiate is generic, type arguments can be provided
after the class name, or they are inferred as for a "diamond"
constructor invocation.  </p>

<p>There is a special syntactic form of constructor references for
arrays, which treats arrays as if they had a constructor that accepts
an <code>int</code> parameter.  For example:</p>

<pre><code>IntFunction&lt;int[]&gt; arrayMaker = int[]::new;
int[] array = arrayMaker.apply(10);  // creates an int[10]
</code></pre>

<h2>10.  Default and static interface methods</h2>

<p>Lambda expressions and method references add a lot of expressiveness to
the Java language, but the key to really achieving our goal of making
code-as-data patterns convenient and idiomatic is to complement these
new features with libraries tailored to take advantage of them.</p>

<p>Adding new functionality to existing libraries is somewhat difficult
in Java SE 7.  In particular, interfaces are essentially set in stone
once they are published; unless one can update all possible
implementations of an interface simultaneously, adding a new method to
an interface can cause existing implementations to break.  The purpose
of <em>default methods</em> (previously referred to as <em>virtual extension
methods</em> or <em>defender methods</em>) is to enable interfaces to be evolved
in a compatible manner after their initial publication.</p>

<p>To illustrate, the standard collections API obviously ought to provide
new lambda-friendly operations. For example, the <code>removeAll</code> method
could be generalized to remove any of a collection's elements for which
an arbitrary property held, where the property was expressed as an
instance of a functional interface <code>Predicate</code>.  But where would this
new method be defined?  We can't add an abstract method to the
<code>Collection</code> interface -- many existing implementations wouldn't know
about the change. We could make it a static method in the <code>Collections</code>
utility class, but that would relegate these new operations to a sort of
second-class status.</p>

<p><em>Default methods</em> provide a more object-oriented way to add concrete
behavior to an interface.  These are a new kind of method: interface
method can either be <em>abstract</em> or <em>default</em>.  Default methods have an
implementation that is inherited by classes that do not override it
(see the next section for the details).  Default methods in a
functional interface don't count against its limit of one abstract
method.  For example, we could have (though did not) add a <code>skip</code>
method to <code>Iterator</code>, as follows:</p>

<pre><code>interface Iterator&lt;E&gt; {
    boolean hasNext();
    E next();
    void remove();

    default void skip(int i) {
        for (; i &gt; 0 &amp;&amp; hasNext(); i--) next();
    }
}
</code></pre>

<p>Given the above definition of <code>Iterator</code>, all classes that implement
<code>Iterator</code> would inherit a <code>skip</code> method.  From a client's perspective,
<code>skip</code> is just another virtual method provided by the interface.  Invoking
<code>skip</code> on an instance of a subclass of <code>Iterator</code> that does not provide a body for
 <code>skip</code> has the effect of invoking the default implementation:
calling <code>hasNext</code> and <code>next</code> up to a certain number of times.  If a
class wants to override <code>skip</code> with a better implementation -- by
advancing a private cursor directly, for example, or incorporating an
atomicity guarantee -- it is free to do so.  </p>

<p>When one interface extends another, it can add a default to an
inherited abstract method, provide a new default for an inherited
default method, or reabstract a default method by redeclaring the
method as abstract.</p>

<p>In addition to allowing code in interfaces in the form of default
methods, Java SE 8 also introduces the ability to place <em>static</em>
methods in interfaces as well.  This allows helper methods that are
specific to an interface to live with the interface, rather than in a
side class (which is often named for the plural of the interface).
For example, <code>Comparator</code> acquired static helper methods for making
comparators, which takes a function that extracts a <code>Comparable</code> sort
key and produces a <code>Comparator</code>:</p>

<pre><code>public static &lt;T, U extends Comparable&lt;? super U&gt;&gt; 
Comparator&lt;T&gt; comparing(Function&lt;T, U&gt; keyExtractor) {
    return (c1, c2) -&gt; keyExtractor.apply(c1).compareTo(keyExtractor.apply(c2));
}
</code></pre>

<h2>11.  Inheritance of default methods</h2>

<p>Default methods are inherited just like other methods; in most cases,
the behavior is just as one would expect.  However, when a class's or
interface's supertypes provide multiple methods with the same
signature, the inheritance rules attempt to resolve the conflict.  Two
basic principles drive these rules:</p>

<ul>
<li><p>Class method declarations are preferred to interface defaults.  This is true
whether the class method is concrete or abstract.  (Hence the <code>default</code>
keyword: default methods are a fallback if the class hierarchy doesn't
say anything.)</p></li>
<li><p>Methods that are already overridden by other candidates are ignored.
This circumstance can arise when supertypes share a common ancestor.</p></li>
</ul>

<p>As an example of how the second rule comes into play, say the
<code>Collection</code> and <code>List</code> interfaces provided different defaults for
<code>removeAll</code>, and <code>Queue</code> inherits the default method from
<code>Collection</code>; in the following <code>implements</code> clause, the <code>List</code>
declaration would have priority over the <code>Collection</code> declaration
inherited by <code>Queue</code>:</p>

<pre><code>class LinkedList&lt;E&gt; implements List&lt;E&gt;, Queue&lt;E&gt; { ... }
</code></pre>

<p>In the event that two independently-defined defaults conflict, or a
default method conflicts with an abstract method, it is a compilation
error.  In this case, the programmer must explicitly override the
supertype methods.  Often, this amounts to picking the preferred
default, and declaring a body that invokes the preferred default.  An
enhanced syntax for <code>super</code> supports the invocation of a particular
superinterface's default implementation:</p>

<pre><code>interface Robot implements Artist, Gun {
    default void draw() { Artist.super.draw(); }
}
</code></pre>

<p>The name preceding <code>super</code> must refer to a direct superinterface that
defines or inherits a default for the invoked method. This form of
method invocation is not restricted to simple disambiguation -- it can
be used just like any other invocation, in both classes and
interfaces.</p>

<p>In no case does the order in which interfaces are declared in an
<code>inherits</code> or <code>extends</code> clause, or which interface was implemented
"first" or "more recently", affect inheritance.</p>

<h2>12.  Putting it together</h2>

<p>The language and library features for Project Lambda were designed to
work together.  To illustrate, we'll consider the task of sorting a
list of people by last name.</p>

<p>Today we write:</p>

<pre><code>List&lt;Person&gt; people = ...
Collections.sort(people, new Comparator&lt;Person&gt;() {
    public int compare(Person x, Person y) {
        return x.getLastName().compareTo(y.getLastName());
    }
});
</code></pre>

<p>This is a very verbose way to write "sort people by last name"!  </p>

<p>With lambda expressions, we can make this expression more concise:</p>

<pre><code>Collections.sort(people, 
                 (Person x, Person y) -&gt; x.getLastName().compareTo(y.getLastName()));
</code></pre>

<p>However, while more concise, it is not any more abstract; it still
burdens the programmer with the need to do the actual comparison
(which is even worse when the sort key is a primitive).  Small changes
to the libraries can help here, such the static <code>comparing</code> method
added to <code>Comparator</code>:</p>

<pre><code>Collections.sort(people, Comparator.comparing((Person p) -&gt; p.getLastName()));
</code></pre>

<p>This can be shortened by allowing the compiler to infer the type
of the lambda parameter, and importing the <code>comparing</code> method via a
static import:</p>

<pre><code>Collections.sort(people, comparing(p -&gt; p.getLastName()));
</code></pre>

<p>The lambda in the above expression is simply a forwarder for the
existing method <code>getLastName</code>.  We can use method references to reuse
the existing method in place of the lambda expression:</p>

<pre><code>Collections.sort(people, comparing(Person::getLastName));
</code></pre>

<p>Finally, the use of an ancillary method like <code>Collections.sort</code> is
undesirable for many reasons: it is more verbose; it can't be specialized
for each data structure that implements <code>List</code>; and it undermines the
value of the <code>List</code> interface since users can't easily discover the
static <code>sort</code> method when inspecting the documentation for <code>List</code>.</p>

<p>Default methods provide a more object-oriented solution for this
problem, where we've added a <code>sort()</code> method to <code>List</code>:</p>

<pre><code>people.sort(comparing(Person::getLastName));
</code></pre>

<p>Which also reads much more like to the problem statement in the first
place: sort the <code>people</code> list by last name.</p>

<p>If we add a default method <code>reversed()</code> to <code>Comparator</code>, which
produces a <code>Comparator</code> that uses the same sort key but in reverse
order, we can just as easily express a descending sort:</p>

<pre><code>people.sort(comparing(Person::getLastName).reversed());
</code></pre>

<h2>13.  Summary</h2>

<p>Java SE 8 adds a relatively small number of new language features --
lambda expressions, method references, default and static methods in
interfaces, and more widespread use of type inference.  Taken
together, though, they enable programmers to express their intent more
clearly and concisely with less boilerplate, and enable the
development of more powerful, parallel-friendly libraries.  </p>

<!-- This document is in Markdown format:
[title]: State of the Lambda
 -->
</body></html>
