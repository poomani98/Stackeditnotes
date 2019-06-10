---


---

<h1 id="angular-concepts">Angular concepts</h1>
<h2 id="dependency-injection">Dependency Injection</h2>
<p>Dependency injection is decoupling classes from what they depend on. i.e. decoupling the creation of an object inside the class that depend on it. This enables us to change the dependency without changing the dependent class.<br>
Basically what we do is, we inject the dependency to the component of the class. Here’s an example,</p>
<pre><code>public Service{
	void serve(){
		print("You're being served");
	}
}
public Customer{
	private Service service;
	public Customer(){
		//dependency
		this.service = new Service();
		//any in change in service class affects it.
	}
	public getService(){
		service.serve();
	}
}
main(){
	Customercustomer = new Customer(); //depends on Service class.
	customer.getService(); 
}
</code></pre>
<p>When dependency injection is introduced,</p>
<pre><code>public Service{
	void serve(){
		print("You're being served");
	}
}
public Customer{
	private Service service;
	public Customer(Service service){
		//dependency is resolved
		this.service = service;
		//any in change in service class requires the injector to handle it before injection.
		//This class need not change the code.
	}
	public getService(){
		service.serve();
	}
}
main(){
	Service service = new Service(); //we collect the resources required and we inject it.
	Customer customer = new Customer(service); //dependency is injected.
	customer.getService(); 
}
</code></pre>
<p>Dependency injection actually helps in</p>
<ul>
<li>Reusing the code.</li>
<li>Testing each of the classes independently.</li>
</ul>
<h3 id="ways-of-injecting-dependency">Ways of injecting dependency</h3>
<ul>
<li>Interfaces</li>
<li>Constructors</li>
<li>Getter &amp; Setter methods</li>
</ul>
<h2 id="data-binding">Data Binding</h2>
<p>Property binding is passing data from and to the <strong>Model</strong> and <strong>View</strong> and vice-versa.</p>
<h3 id="types-of-data-binding">Types of data binding</h3>

<table>
<thead>
<tr>
<th>Binding</th>
<th>Direction</th>
<th>Operator</th>
</tr>
</thead>
<tbody>
<tr>
<td>Property Binding</td>
<td>Model --&gt; View</td>
<td><code>[ ]</code></td>
</tr>
<tr>
<td>Interpolation</td>
<td>Model --&gt; View</td>
<td><code>{{ }}</code></td>
</tr>
<tr>
<td>Event Binding</td>
<td>Model --&gt; View</td>
<td><code>( )</code></td>
</tr>
<tr>
<td>Two way Binding</td>
<td>Model &lt;-&gt; View</td>
<td><code>[( )]</code></td>
</tr>
</tbody>
</table><h4 id="property-binding">Property binding</h4>
<p>.html file:</p>
<pre><code>&lt;button [disabled]="boolVarName"&gt;Click!&lt;/button&gt;
</code></pre>
<p>.ts file:</p>
<pre><code>boolVarName = true;
</code></pre>
<p>Using square brackets around the HTML attribute and assigning it any variable in the class file, any changes to the variable in the class file will reflect in the view.</p>
<h4 id="interpolation">Interpolation</h4>
<p>.html file:</p>
<pre><code>&lt;h1&gt;{{varName}}&lt;/h1&gt;
</code></pre>
<p>.ts file:</p>
<pre><code>varName = "This is a heading tag";
</code></pre>
<p>However, Interpolation can only work with HTML attribute that accepts string inputs. The above example in Property binding cannot be done using Interpolation.</p>
<h4 id="event-binding">Event binding</h4>
<pre><code>&lt;button (click)="methodName()"&gt;Do Something&lt;/button&gt;
</code></pre>
<p>Click event on the button will invoke the method it is tied to.</p>
<h4 id="two-way-binding">Two-way binding</h4>
<pre><code>&lt;h1&gt;{{heading}}&lt;/h1&gt;
&lt;input [(NgModel)]="heading" /&gt;
</code></pre>
<p>Any changes that are made to the variable <code>heading</code> by the <strong>model</strong> will be reflected in the <strong>view</strong> as well as the changes made in the <strong>view</strong> will be reflected in the <strong>model</strong>.</p>
<h1 id="template-driven-forms">Template driven forms</h1>
<p>Whenever a form is created in angular provides the form with an angular directive called <strong>ngForm</strong> this supplements many features such as <em>values</em>, <em>valid</em>, <em>pristine</em>, <em>touched</em>, <em>dirty</em>, etc.</p>
<p>First we need to import <code>FormsModule</code> from <code>"@angular/forms"</code> in <code>app.module.ts</code>.</p>
<pre><code>&lt;form #formVar = "ngForm" [(ngSubmit)]="onSubmit(formVar)"&gt;
	&lt;input name="studentName" type="text" name = "Student" [(ngModel)] = "nameVar"&gt;
	&lt;input name="rollNo" type="text" name = "RollNo" [(ngModel)] = "rollVar"&gt;
	&lt;input type="submit" &gt;
&lt;/form&gt;
</code></pre>
<p>The variable <code>formVar</code> holds a reference to <code>ngForm</code> any changes made to the form will be reflected in the <code>formVar</code> variable.<br>
On submitting the form the  template reference variable<br>
<code>formVar</code> is passed to the method <code>onSubmit(form : ngForm)</code>where we can make use of the form data.</p>
<h2 id="directives">Directives</h2>
<h3 id="ngif">ngIf</h3>
<p>Shorthand:</p>
<pre><code>&lt;div *ngIf="condition"&gt;Content to render if true&lt;/div&gt;
</code></pre>
<p><code>"condition"</code> is replaced with a any typescript statement or expression.<br>
If the expression returns <code>true</code> then the template(HTML tag) containing the <code>ngIf</code> is rendered.</p>
<p>Expanded syntax:</p>
<pre><code>&lt;ng-template [ngIf]="condition"&gt;&lt;div&gt;Content to render if true&lt;/div&gt;&lt;/ng-template&gt;
</code></pre>
<h4 id="ngif---else">ngIf - else</h4>
<pre><code>&lt;div *ngIf="condition; else elseBlock"&gt;Content to render if true.&lt;/div&gt;
&lt;ng-template #elseBlock&gt;Content to render if false.&lt;/ng-template&gt;
</code></pre>
<h4 id="ngif---then---else">ngIf - then - else</h4>
<pre><code>&lt;div *ngIf="condition; then thenBlock else elseBlock"&gt;&lt;/div&gt;
&lt;ng-template #thenBlock&gt;Content to render when condition is true.&lt;/ng-template&gt;
&lt;ng-template #elseBlock&gt;Content to render when condition is false.&lt;/ng-template&gt;
</code></pre>
<h3 id="ngfor">ngFor</h3>
<p>ngFor is used for used for looping and displaying list items into the HTML page.</p>
<p>Shorthand syntax:</p>
<pre><code>&lt;ul&gt;
	&lt;li *ngFor="let value of listOfvalues; index as i;"&gt;{{ value }}&lt;/li&gt;
&lt;/ul&gt;
</code></pre>
<p>Here <code>i</code> gives the index and <code>value</code> variable holds each and every element of the list <code>listOfvalues</code>.</p>

