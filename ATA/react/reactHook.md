`<h2 id="react-hook-出现背景" data-spm-anchor-id="ata.21736010.0.i67.23c65140M45Q5a"><code data-spm-anchor-id="ata.21736010.0.i60.23c65140M45Q5a">React Hook</code> 出现背景</h2>

<h3 id="类组件的问题">类组件的问题</h3>
<ul>
<li data-spm-anchor-id="ata.21736010.0.i1.23c65140M45Q5a">复用组件状态难，高阶组件+渲染属性 <code>providers customers</code>，等一堆工具都是为了解决这个问题，但是造成了很严重的理解成本和组件嵌套地狱</li>
<li>生命周期带来的负面影响，逻辑拆分严重</li>
<li data-spm-anchor-id="ata.21736010.0.i2.23c65140M45Q5a">This 的指向问题</li>
</ul>
<h3 id="函数组件的局限">函数组件的局限</h3>
<ul>
<li data-spm-anchor-id="ata.21736010.0.i3.23c65140M45Q5a">之前函数组件没有 <code>state</code> 和 生命周期，导致使用场景有限</li>
</ul>
<h3 id="react-hook">React Hook</h3>
<p><code>Hooks</code> 是 <code>React 16.8</code> 新增的特性，它可以让你在不编写 <code>class</code> 的情况下使用 <code>state</code> 以及其他的 <code>React</code> 特性，无需转化成类组件</p>
<h2 id="hook-的使用和实践"><code>Hook</code> 的使用和实践</h2>
<h3 id="usestate-和-hook-的闭包机制"><code>useState</code> 和 <code>Hook</code> 的闭包机制</h3>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i11.23c65140M45Q5a"><code class="language-js" style="white-space: pre;"><span style="color: rgb(153, 153, 136); font-style: italic;">// hook 组件</span><span>
</span><span></span><span class="hljs-function" style="color: rgb(51, 51, 51); font-weight: bold;">function</span><span class="hljs-function"> </span><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">Counter</span><span class="hljs-function">(</span><span class="hljs-function">) </span><span>{
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> [count, setCount] = useState(</span><span style="color: rgb(0, 128, 128);">0</span><span>);
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> log = </span><span class="hljs-function">() =&gt;</span><span data-spm-anchor-id="ata.21736010.0.i8.23c65140M45Q5a"> {
</span><span>    setCount(count + </span><span style="color: rgb(0, 128, 128);">1</span><span>);
</span><span>    </span><span style="color: rgb(0, 134, 179);">setTimeout</span><span>(</span><span class="hljs-function" data-spm-anchor-id="ata.21736010.0.i9.23c65140M45Q5a">() =&gt;</span><span> {
</span><span>      </span><span style="color: rgb(0, 134, 179);" data-spm-anchor-id="ata.21736010.0.i10.23c65140M45Q5a">console</span><span>.log(count);
</span><span>    }, </span><span style="color: rgb(0, 128, 128);">3000</span><span>);
</span>  };
<span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> (
</span><span>    </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">div</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">
</span><span class="xml">      </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">p</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">You&nbsp;clicked&nbsp;{count}&nbsp;times</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">p</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">
</span><span class="xml">      </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">button</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;"> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">onClick</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">=</span><span class="xml" style="color: rgb(221, 17, 68); font-weight: normal;">{log}</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">Click&nbsp;me</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">button</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">&nbsp;&nbsp;&nbsp;
</span><span class="xml">    </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">div</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span>
</span>  );
}

<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 等效的类组件</span><span>
</span><span></span><span class="hljs-class" style="color: rgb(51, 51, 51); font-weight: bold;">class</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">Counter</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(51, 51, 51); font-weight: bold;">extends</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;" data-spm-anchor-id="ata.21736010.0.i4.23c65140M45Q5a">Component</span><span class="hljs-class"> </span><span>{
</span><span> state = { </span><span>count</span><span>: </span><span style="color: rgb(0, 128, 128);">0</span><span> };
</span><span> log = </span><span class="hljs-function">() =&gt;</span><span> {
</span><span> </span><span style="color: rgb(0, 134, 179);">this</span><span>.setState({
</span><span> </span><span>count</span><span>: </span><span style="color: rgb(0, 134, 179);">this</span><span>.state.count + </span><span style="color: rgb(0, 128, 128);">1</span><span>,
</span> });
<span> </span><span style="color: rgb(0, 134, 179);">setTimeout</span><span>(</span><span class="hljs-function">() =&gt;</span><span> {
</span><span data-spm-anchor-id="ata.21736010.0.i14.23c65140M45Q5a"> </span><span style="color: rgb(0, 134, 179);">console</span><span>.log(</span><span style="color: rgb(0, 134, 179);">this</span><span>.state.count);
</span><span> }, </span><span style="color: rgb(0, 128, 128);">3000</span><span data-spm-anchor-id="ata.21736010.0.i13.23c65140M45Q5a">);
</span> };
<span> </span><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">render</span><span class="hljs-function">(</span><span class="hljs-function">)</span><span> {
</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> (
</span><span> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">div</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">
</span><span class="xml"> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">p</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml" data-spm-anchor-id="ata.21736010.0.i12.23c65140M45Q5a">You&nbsp;clicked&nbsp;{this.state.count}&nbsp;times</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">p</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">
</span><span class="xml"> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">button</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;"> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">onClick</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">=</span><span class="xml" style="color: rgb(221, 17, 68); font-weight: normal;">{this.log}</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">Click&nbsp;me</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">button</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span><span class="xml"> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">div</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span>
</span> );
}
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>

<p>快速点击下的情况下，想想 <code>Hook</code> 组件和函数式组件控制台打印出来的是什么？</p>
<ul>
<li>类组件打印出来的是 <code>3 3 3</code><br><code>Class</code> 组件的 <code>state</code> 是不可变的，通过 <code>setState</code> 返回一个新的引用，<code>this.state</code> 指向一个新的引用<br><code>setTimeout</code> 执行的时候，通过 <code>this</code> 获取最新的 <code>state</code> 引用，所以这个输出都是 <code>3</code></li>
<li>函数组件打印的结果是 <code>0 1 2</code><br>函数组件闭包机制，函数组件每一次渲染都有独立的 <code>props</code> 和 <code>state</code><br>每一次渲染都有独立的事件处理函数<br>每一次渲染的状态不会受到后面事件处理的影响</li>
</ul>
<h3 id="函数组件渲染拆解">函数组件渲染拆解</h3>
<p>既然每次渲染都是一个独立的闭包，可以尝试代码拆解函数式组件的渲染过程</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>// 第一次点击
</span>function&nbsp;Counter()&nbsp;{
<span>&nbsp;&nbsp;const&nbsp;[</span><span style="color: rgb(0, 128, 128);">0</span><span>,&nbsp;setCount]&nbsp;=&nbsp;useState(</span><span style="color: rgb(0, 128, 128);">0</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  const&nbsp;log&nbsp;=&nbsp;()&nbsp;=&gt;&nbsp;{
<span>&nbsp;&nbsp;&nbsp;&nbsp;setCount(</span><span style="color: rgb(0, 128, 128);">0</span><span>&nbsp;+&nbsp;</span><span style="color: rgb(0, 128, 128);">1</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>    // 只能获取这次点击按钮的 state
&nbsp;&nbsp;&nbsp;&nbsp;setTimeout(()&nbsp;=&gt;&nbsp;{
<span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(</span><span style="color: rgb(0, 128, 128);">0</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>&nbsp;&nbsp;&nbsp;&nbsp;},&nbsp;</span><span style="color: rgb(0, 128, 128);">3000</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>&nbsp;&nbsp;}</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
// 第二次点击
function&nbsp;Counter()&nbsp;{
<span>  const&nbsp;[</span><span style="color: rgb(0, 128, 128);">1</span><span>,&nbsp;setCount]&nbsp;=&nbsp;useState(</span><span style="color: rgb(0, 128, 128);">0</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  const&nbsp;log&nbsp;=&nbsp;()&nbsp;=&gt;&nbsp;{
<span>&nbsp;&nbsp;&nbsp;setCount(</span><span style="color: rgb(0, 128, 128);">1</span><span>&nbsp;+&nbsp;</span><span style="color: rgb(0, 128, 128);">1</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>&nbsp;&nbsp;&nbsp;&nbsp;setTimeout(()&nbsp;=&gt;&nbsp;{
<span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(</span><span style="color: rgb(0, 128, 128);">1</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>&nbsp;&nbsp;&nbsp;&nbsp;},&nbsp;</span><span style="color: rgb(0, 128, 128);">3000</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>&nbsp;&nbsp;}</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
// 第三次点击
function&nbsp;Counter()&nbsp;{
<span>  const&nbsp;[</span><span style="color: rgb(0, 128, 128);">2</span><span>,&nbsp;setCount]&nbsp;=&nbsp;useState(</span><span style="color: rgb(0, 128, 128);">0</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;&nbsp;</span><span>
</span>  const&nbsp;log&nbsp;=&nbsp;()&nbsp;=&gt;&nbsp;{
<span>&nbsp;&nbsp;&nbsp;&nbsp;setCount(</span><span style="color: rgb(0, 128, 128);">2</span><span>&nbsp;+&nbsp;</span><span style="color: rgb(0, 128, 128);">1</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>&nbsp;&nbsp;&nbsp;&nbsp;setTimeout(()&nbsp;=&gt;&nbsp;{
<span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(</span><span style="color: rgb(0, 128, 128);">2</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>&nbsp;&nbsp;&nbsp;&nbsp;},&nbsp;</span><span style="color: rgb(0, 128, 128);">3000</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>&nbsp;&nbsp;}</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<ul>
<li><p>三次点击，共 <code>4</code> 次渲染，<code>count</code> 从 <code>0</code> 变为 <code>3</code></p>
</li>
<li><p>页面第一次渲染，页面看到的 <code>count = 0</code></p>
</li>
<li><p>第一次点击，事件处理器获取的 <code>count = 0</code>，<code>count</code> 变成 <code>1</code>， 第二次渲染，渲染后页面看到 <code>count = 1</code>，对应上述代码第一次点击</p>
</li>
<li><p>第二次点击，事件处理器获取的 <code>count = 1</code>，<code>count</code> 变成 <code>2</code>， 第三次渲染，渲染后页面看到 <code>count = 2</code>，对应上述代码第二次点击</p>
</li>
<li><p>第三次点击，事件处理器获取的 <code>count = 2</code>，<code>count</code> 变成 <code>3</code>， 第四次渲染，渲染后页面看到 <code>count = 3</code>，对应上述代码第三次点击</p>
</li>
</ul>
<h3 id="让函数式组件也可以输出-3-3-3">让函数式组件也可以输出 <code>3 3 3</code></h3>
<p>有种比较简单并且能解决问题的方案，借用 <code>useRef</code></p>
<ul>
<li><code>useRef</code> 返回一个可变的 <code>ref</code> 对象，其 &nbsp;<code>current</code>&nbsp; 属性被初始化为传入的参数<code>（initialValue）</code></li>
<li><code>useRef</code> 返回的 <code>ref</code> 对象在组件的整个生命周期内保持不变，也就是说每次重新渲染函数组件时，返回的 <code>ref</code> 对象都是同一个</li>
<li><code>useRef</code> 可以类比成类组件实例化后的 <code>this</code>，在组件没有销毁的返回的引用都是同一个</li>
</ul>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span class="hljs-function" style="color: rgb(51, 51, 51); font-weight: bold;">function</span><span class="hljs-function"> </span><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">Counter</span><span class="hljs-function">(</span><span class="hljs-function">) </span><span>{
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span data-spm-anchor-id="ata.21736010.0.i15.23c65140M45Q5a"> count = useRef(</span><span style="color: rgb(0, 128, 128);">0</span><span>);
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> log = </span><span class="hljs-function">() =&gt;</span><span> {
</span>    count.current++;
<span>    </span><span style="color: rgb(0, 134, 179);">setTimeout</span><span>(</span><span class="hljs-function">() =&gt;</span><span> {
</span><span>      </span><span style="color: rgb(0, 134, 179);">console</span><span>.log(count.current);
</span><span>    }, </span><span style="color: rgb(0, 128, 128);">3000</span><span>);
</span>  };
<span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> (
</span><span>    </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">div</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">
</span><span class="xml">      </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">p</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">You&nbsp;clicked&nbsp;{count.current}&nbsp;times</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">p</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">
</span><span class="xml">      </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">button</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;"> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">onClick</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">=</span><span class="xml" style="color: rgb(221, 17, 68); font-weight: normal;">{log}</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">Click&nbsp;me</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">button</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span class="xml">&nbsp;&nbsp;&nbsp;&nbsp;
</span><span class="xml">    </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;/</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">div</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&gt;</span><span>
</span>  );
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<ul>
<li>这样修改一下，控制台输出的确实是 <code>3 3 3</code></li>
<li>？ 既然 <code>Ref</code> 对象整个生命周期都不变，修改 <code>current</code> 属性也只是修改属性，那除了打印，这里的 <code>You clicked 0 times</code> ，点击三次，会变成 <code>3</code> 么？</li>
<li data-spm-anchor-id="ata.21736010.0.i18.23c65140M45Q5a">显然不能，这个组件没有任何的属性和状态改变，会重新渲染才怪，所以这里虽然点击了 <code>3</code> 次，但是不会像 <code>useState</code> 一样，渲染 <code>4</code> 次，这里只会渲染 <code>1</code> 次，然后看到的都是 <code>You clicked 0 times</code></li>
<li data-spm-anchor-id="ata.21736010.0.i17.23c65140M45Q5a">修复一个问题把另外一个更大的问题引进来，这很程序员。。。</li>
</ul>
<h3 id="useeffect">useEffect</h3>
<p>通过 <code>useRef</code> 虽然能解决打印的问题，但是页面渲染是不对的，这里还是使用 <code>useState</code> 的方案，配合 <code>useEffect</code> 可以实现我们想要的效果</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span style="color: rgb(51, 51, 51); font-weight: bold;">function</span><span>&nbsp;use</span><span class="hljs-constructor">Effect(</span><span class="hljs-constructor hljs-params">effect</span><span class="hljs-constructor">:&nbsp;EffectCallback,&nbsp;</span><span class="hljs-constructor hljs-params">deps</span><span class="hljs-constructor">?:&nbsp;DependencyList)</span><span>:&nbsp;void;</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<ul>
<li>看下 <code>useEffect</code> 的签名，<code>effect</code> 是函数类型，并且必填， 还有第二个可选参数，类型是只读数组</li>
<li><code>useEffect</code>&nbsp; 是处理副作用的，其执行时机在 &nbsp; 每次 <code>Render</code> 渲染完毕后，换句话说就是每次渲染都会执行，在真实 <code>DOM</code> 操作完毕后。</li>
</ul>
<p>配合这个 <code>hook</code>， 如果每次 <code>state</code> 改变后渲染完之后，把 <code>ref</code> 里面的值更新，然后控制台打印 <code>ref</code> 的值</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>function Counter() {
</span><span>  const [count, setCount] = useState(</span><span style="color: rgb(0, 128, 128);">0</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  const currentCount = useRef(</span><span style="color: rgb(0, 134, 179); font-weight: normal;">count</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  useEffect(() =&gt; {
    currentCount.current = count;
<span>  })</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  const log = () =&gt; {
<span>    setCount(</span><span style="color: rgb(0, 134, 179); font-weight: normal;">count</span><span> + </span><span style="color: rgb(0, 128, 128);">1</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>    setTimeout(() =&gt; {
<span>      console.log(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">currentCount.current</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>    }, </span><span style="color: rgb(0, 128, 128);">3000</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  return (
    &lt;div&gt;
      &lt;p&gt;You&nbsp;clicked&nbsp;{count}&nbsp;times&lt;/p&gt;
      &lt;button onClick={log}&gt;Click&nbsp;me&lt;/button&gt; &nbsp;&nbsp;&nbsp;&nbsp;
    &lt;/div&gt;
<span>  )</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>这样子写可以符合我们的预期效果，页面展示从 <code>0 1 2 3</code>， 然后控制台输出 <code>3 3 3</code>，然后我们拆解下渲染过程。</p>
<ul>
<li>三次点击，共 <code>4</code> 次渲染，<code>count</code> 从 <code>0</code> 变为 <code>3</code></li>
<li>页面初始化渲染，<code>count = 0</code>， <code>currentCount.current = 0</code>， 页面显示 <code>0</code>， 渲染完成，触发 <code>useEffect</code>， <code>currentCount.current = 0</code></li>
<li>第一次点击，<code>count = 0</code>， 渲染完成后，<code>count = 1</code>， 页面显示 <code>1</code>，触发 <code>useEffect</code>，<code>currentCount.current = 1</code></li>
<li>第二次点击，<code>count = 1</code>， 渲染完成后，<code>count = 2</code>， 页面显示 <code>2</code>，触发 <code>useEffect</code>，<code>currentCount.current = 2</code></li>
<li>第三次点击，<code>count = 2</code>， 渲染完成后，<code>count = 3</code>， 页面显示 <code>3</code>，触发 <code>useEffect</code>，<code>currentCount.current = 3</code></li>
<li>三次点击完成，<code>currentCount.current = 3</code>，第四次渲染，页面看到 <code>count = 3</code>， <code>setTimeout</code> 中调用的是 <code>currentCount</code> 这个对象，输出都是 <code>3</code></li>
</ul>
<h3 id="useeffect-的函数返回值"><code>useEffect</code> 的函数返回值</h3>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>type EffectCallback = </span><span class="hljs-function hljs-params">()</span><span class="hljs-function"> =&gt;</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">void</span><span> | (</span><span class="hljs-function hljs-params">()</span><span class="hljs-function"> =&gt;</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">void</span><span> | </span><span style="color: rgb(0, 128, 128);">undefined</span><span>);</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p><code>useEffect</code> 的回调函数可以返回空，也可以返回一个函数，如果返回一个函数的话，在 <code>effect</code> 执行回调函数的时候，会先执行上一次 <code>effect</code> 回调函数返回的函数</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>useEffect(() =&gt; {
</span><span>  console.log(</span><span style="color: rgb(153, 0, 115);">'after</span><span> render')</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  return () =&gt; {
<span>    console.log(</span><span style="color: rgb(153, 0, 115);">'last</span><span> time effect return')</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>})</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>这个 <code>useEffect</code> ，每次渲染完之后，控制台会先输出 <code>last time effect return</code>，然后再输出 <code>after render</code></p>
<h3 id="useeffect-和-类组件生命周期">useEffect 和 类组件生命周期</h3>
<p>之前提到，<code>useEffct</code> 有两个参数，第二参数是个可选参数，是 <code>effect</code> 的依赖列表， <code>React</code> 根据这些列表的值是否有改变，决定渲染完之后，是否执行这个副作用的回调</p>
<p>如果不传这个参数，<code>React</code> 会认为这个 <code>effect</code> 每次渲染然之后都要执行，等同于 <code>componentDidUpdate</code> 这个生命周期无约束执行</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">useEffect</span><span class="hljs-function hljs-params">(()</span><span> =&gt; {
</span><span>  currentCount</span><span class="hljs-selector-class">.current</span><span> = count;
</span>});
<span></span><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">componentDidUpdate</span><span class="hljs-function hljs-params">()</span><span>&nbsp;{
</span><span>&nbsp;&nbsp;currentCount</span><span class="hljs-selector-class">.current</span><span>&nbsp;=&nbsp;this</span><span class="hljs-selector-class">.state</span><span>.count;
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>如果这个参数是空数组，<code>React</code> 会认为组件内任何状态和属性改变，都不会触发这个 <code>effect</code>，相当于这个 <code>effect</code> 是仅仅在组件渲染完之后，执行一次，后面组件任何更新都不会触发这个 <code>effect</code>，等同 <code>componentDidMount</code></p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">useEffect</span><span class="hljs-function hljs-params">(()</span><span> =&gt; {
</span><span>  currentCount</span><span class="hljs-selector-class">.current</span><span> = count;
</span><span>}, </span><span class="hljs-selector-attr">[]</span><span>);
</span><span></span><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">componentDidMount</span><span class="hljs-function hljs-params">()</span><span>&nbsp;{
</span><span>&nbsp;&nbsp;currentCount</span><span class="hljs-selector-class">.current</span><span>&nbsp;=&nbsp;this</span><span class="hljs-selector-class">.state</span><span>.count;
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>如果配合 <code>useEffect</code> 回调函数的返回函数，可以实现类似 <code>componentWillUnmount</code> 的效果，因为如果是空数组的话，组件任何更新都不会触发 <code>effect</code>，所以回调函数的返回函数只能在组件销毁的时候执行</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>useEffect(() =&gt; {
</span>  return () =&gt; {
<span>    console.log(</span><span style="color: rgb(153, 0, 115);">'will</span><span> trigger ar willUnmount')
</span>  }
<span>}, [])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>componentWillUnmount() {
<span>  console.log(</span><span style="color: rgb(153, 0, 115);">'will</span><span> trigger ar willUnmount')
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>如果依赖列表里面有值，则类似<code>componentDidMount</code>有条件约束更新，只有当上一次的状态和这次的不一样，才执行</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">useEffect</span><span class="hljs-function hljs-params">(()</span><span> =&gt; {
</span><span>  currentCount</span><span class="hljs-selector-class">.current</span><span> = count;
</span><span>}, </span><span class="hljs-selector-attr">[count]</span><span>);
</span><span></span><span class="hljs-function" style="color: rgb(153, 0, 0); font-weight: bold;">componentDidUpdate</span><span class="hljs-function hljs-params">(prevProps, prevState)</span><span>&nbsp;{
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">if</span><span> (prevState</span><span class="hljs-selector-class">.count</span><span> !== this</span><span class="hljs-selector-class">.state</span><span>.count) {
</span><span>    currentCount</span><span class="hljs-selector-class">.current</span><span>&nbsp;=&nbsp;this</span><span class="hljs-selector-class">.state</span><span>.count;
</span>  }
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="useeffect-和-闭包问题"><code>useEffect</code> 和 闭包问题</h3>
<p>假设组件需要在初始化的时候，定义一个定时器，让 <code>count</code> 自增，自然而然的可以写出以下的代码</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>// 初始化的 count = </span><span style="color: rgb(0, 128, 128);">0</span><span>
</span>useEffect(() =&gt; {
  const id = setInterval(() =&gt; {
<span>    setCount(</span><span style="color: rgb(0, 134, 179); font-weight: normal;">count</span><span> + </span><span style="color: rgb(0, 128, 128);">1</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }, </span><span style="color: rgb(0, 128, 128);">1000</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>}, [])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>componentDidMount()&nbsp;{
&nbsp;&nbsp;setInterval(()&nbsp;=&gt;&nbsp;{
<span>&nbsp;&nbsp;  this.setState({&nbsp;count:&nbsp;this.state.count&nbsp;+&nbsp;</span><span style="color: rgb(0, 128, 128);">1</span><span>&nbsp;})</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>&nbsp;&nbsp;},&nbsp;</span><span style="color: rgb(0, 128, 128);">1000</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>但是实际运行的时候，类组件展示是对的，函数组件从 <code>0</code> 递增到 <code>1</code> 之后，页面渲染就再也不变了</p>
<ul>
<li>之前有提过，类组件因为有 <code>this</code> 这个引用，很容易通过 <code>state</code> 拿到最新的值</li>
<li>函数组件每次渲染都是独立的闭包，这里因为写的依赖值是 <code>[]</code>，所以只有首次渲染后，才会这行这个 <code>effect</code>，首次渲染后， <code>count</code> 就是 <code>0</code>，所以 <code>setCount(count + 1)</code> 每次都是执行 <code>setCount(0 + 1)</code>，所以定时器工作是正常的，不过取的值有问题。</li>
</ul>
<h3 id="闭包问题的切入点和发生场景">闭包问题的切入点和发生场景</h3>
<p>闭包问题，大多发生在，有些回调函数执行，依赖到组件的某些状态，但是这些状态并没有写到 <code>useEffect</code> 的依赖列表里面。导致执行回调函数的时候，拿到组件的状态不是最新的。<br>主要的场景有：</p>
<ul>
<li>定时器</li>
<li>事件监听的回调</li>
<li>各种 <code>Observer</code> 的回调</li>
</ul>
<p>这些场景，通常只要在组件初始化渲染完之后，定义一次回调函数就好，但是如果回调函数依赖到组件的转态或者属性，这时候就要小心，闭包问题</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i5.23c65140M45Q5a"><code class="language-ts" style="white-space: pre;"><span>function Router() {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, </span><span style="color: rgb(0, 134, 179);">set</span><span>State] = useState</span><span style="color: rgb(0, 128, 128);">&lt;string&gt;</span><span>('');
</span>  useEffect(() =&gt; {
<span>    window.addEventListener</span><span style="color: rgb(0, 128, 128);">&lt;'hashchange'&gt;</span><span>(
</span>      'hashchange',
      () =&gt; {
<span>        // 监听 hash 变化，这里依赖到 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>
</span>      },
      false
    );
  }, []);
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>例如这里的写法，在组件渲染完监听 <code>hashchange</code> ，回调函数是拿不到后续更新的 <code>state</code> 的，只能能到初始化时候的空字符串。</p>
<h3 id="尝试解决闭包问题-监听state变化">尝试解决闭包问题-监听<code>state</code>变化</h3>
<p>既然回调函数要每次都拿到最新的 <code>state</code>，可以监听 <code>state</code> 的变化，<code>state</code> 变化的时候，重新定义事件监听器，改写一下</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-ts" style="white-space: pre;"><span>function Router() {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, </span><span style="color: rgb(0, 134, 179);">set</span><span>State] = useState</span><span style="color: rgb(0, 128, 128);">&lt;string&gt;</span><span>('');
</span>  useEffect(() =&gt; {
    window.addEventListener(
      'hashchange',
      () =&gt; {
<span>        // 监听 hash 变化，这里依赖到 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>
</span>      },
      false
    );
<span>  }, [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>]);
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>以上代码能用，但是 <code>state</code> 每次改变，就会重新定义一个 <code>hashchange</code> 回调函数，但是上一次的 <code>hashchange</code> 的事件监听器并没有清除，代码能跑，但是内存泄漏也太严重了，可以配合 <code>useEffect</code> 回调函数返回的函数配合清掉上一次的事件监听器</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-ts" style="white-space: pre;"><span>function Router() {
</span><span>  const [</span><span style="color: rgb(0, 0, 128); font-weight: normal;">state</span><span>, setState] = useState&lt;string&gt;('')</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  useEffect(() =&gt; {
<span>    const callback = () =&gt; {}</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>    window.addEventListener(</span><span style="color: rgb(153, 0, 115);">'hashchange</span><span>', callback, false)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>    return () =&gt; window.removeEventListener(</span><span style="color: rgb(153, 0, 115);">'hashchange</span><span>', callback, false)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }, [</span><span style="color: rgb(0, 0, 128); font-weight: normal;">state</span><span>])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>这样内存泄漏的问题被解决了，但是这种事情监听，正常来说设置一次就好，没必要重新定义，还有别的更好的方法么？</p>
<h3 id="尝试解决闭包问题---setstate-另外一种更新组件状态的方式">尝试解决闭包问题 - <code>setState</code> 另外一种更新组件状态的方式</h3>
<p><code>useState</code> 返回的更新状态的函数，除了可以传一个值，还可以传一个回调函数，回调函数带一个参数，这个参数是最新的 <code>state</code>，像这样的话，之前那个定时器的例子，可以修改成这样。</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i19.23c65140M45Q5a"><code class="language-ts" style="white-space: pre;" data-spm-anchor-id="ata.21736010.0.i20.23c65140M45Q5a"><span>function Counter() {
</span><span>  const [count, setCount] = useState(</span><span style="color: rgb(0, 128, 128);">0</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  useEffect(() =&gt; {
    const id = setInterval(() =&gt; {
<span>      // setCount(</span><span style="color: rgb(0, 134, 179); font-weight: normal;">count</span><span> + </span><span style="color: rgb(0, 128, 128);">1</span><span>)
</span><span>      setCount((</span><span style="color: rgb(0, 0, 128); font-weight: normal;">c</span><span>) =&gt; c + </span><span style="color: rgb(0, 128, 128);">1</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>    }, </span><span style="color: rgb(0, 128, 128);">1000</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>    return () =&gt; clearInterval(</span><span style="color: rgb(0, 134, 179); font-weight: normal;">id</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }, [])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  return &lt;h1&gt;{count}&lt;/h1&gt;;
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p data-spm-anchor-id="ata.21736010.0.i21.23c65140M45Q5a">这里我们改了一行代码，<code>setCount(count + 1)</code> 改成了 <code>setCount((c) =&gt; c + 1)</code>，这样修改之后，其实定时器回调已经没有依赖到 <code>count</code> 这个值了，由 <code>setCount</code> 里面的回调函数，返回最新的 <code>count</code> 的值，就是<code>setCount((c) =&gt; c + 1)</code>，里面的 <code>c</code>.</p>
<p data-spm-anchor-id="ata.21736010.0.i22.23c65140M45Q5a">同样的，对于事件监听器里面，我们也可以通过这个方式去获取最新的 <code>state</code>，但是这里有几个问题</p>
<ul>
<li>这个回调函数，其实也只要获取最新的 <code>state</code>，所以在调用 <code>setState</code> 的时候，拿到最新的值的同时，记得把 <code>setState</code> 的值，设置成和当前同一个，如果没有返回，那调用 <code>setState</code> 之后， <code>state</code> 的值会变成 <code>undefined</code></li>
<li data-spm-anchor-id="ata.21736010.0.i31.23c65140M45Q5a"><code>setState</code> 返回一个同样的值，会不会导致组件和它的子组件重新渲染？找了下文档说明是这样的：调用 State Hook 的更新函数并传入当前的 state 时，React 将跳过子组件的渲染及 effect 的执行。需要注意的是，React 可能仍需要在跳过渲染前渲染该组件。不过由于 React 不会对组件树的“深层”节点进行不必要的渲染，所以大可不必担心</li>
<li data-spm-anchor-id="ata.21736010.0.i63.23c65140M45Q5a">看起来可行的，做一下简单的修改其实可以改成这样</li>
</ul>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i25.23c65140M45Q5a"><code class="language-ts" style="white-space: pre;" data-spm-anchor-id="ata.21736010.0.i26.23c65140M45Q5a"><span>function Router() {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, </span><span style="color: rgb(0, 134, 179);">set</span><span>State] = useState</span><span style="color: rgb(0, 128, 128);">&lt;string&gt;</span><span>('');
</span>  useEffect(() =&gt; {
<span>    </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> callback = () =&gt; {
</span>      let latestState = ‘’;
<span data-spm-anchor-id="ata.21736010.0.i24.23c65140M45Q5a">      </span><span style="color: rgb(0, 134, 179);">set</span><span>State((</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span data-spm-anchor-id="ata.21736010.0.i32.23c65140M45Q5a">Callback) =&gt; {
</span><span data-spm-anchor-id="ata.21736010.0.i33.23c65140M45Q5a">        // </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>Callback 是最新的 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>
</span><span data-spm-anchor-id="ata.21736010.0.i29.23c65140M45Q5a">        latestState = </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>Callback;
</span><span data-spm-anchor-id="ata.21736010.0.i27.23c65140M45Q5a">        // 记得把 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>Callback 返回去，不然 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span> 会被改成 undefined
</span><span>        return </span><span style="color: rgb(51, 51, 51); font-weight: bold;" data-spm-anchor-id="ata.21736010.0.i28.23c65140M45Q5a">state</span><span>Callback;
</span>      });
<span data-spm-anchor-id="ata.21736010.0.i30.23c65140M45Q5a">      // latestState 已经被赋值为最新的 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span> 了
</span>    }；
<span>    window.addEventListener</span><span style="color: rgb(0, 128, 128);">&lt;'hashchange'&gt;</span><span>('hashchange', callback, false);
</span>  }, [])
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p data-spm-anchor-id="ata.21736010.0.i23.23c65140M45Q5a">这样基本就没问题了，做到了只定义了一次回调，然后也可以获取最新的 <code>state</code>，一举两得，但是还是有问题的</p>
<ul>
<li><p><code>setState</code> 回调函数如果不写 <code>return stateCallback;</code> 这段代码，会导致 <code>state</code> 莫名其妙被设置成 <code>undefined</code> ，而且非常不好发现，维护性太差</p>
</li>
<li><p><code>setState</code> 是用来改变组件的 <code>state</code> 的，不是让你这样用的的，虽然这样用完全没问题。但是可维护性太差了，如果你的代码被接手，别人就会疑惑这里为什么要这么写，无注释和变量命名太糟糕的情况下，代码可以维护性基本为 <code>0</code></p>
</li>
<li><p>设置一个同样的 <code>state</code>，虽然不会导致子组件重新渲染，但是本组件还是有可能重新渲染的，按官网的说法</p>
</li>
</ul>
<p>这个方案不完美。思路再发散一下？执行回调函数的时候，需要获取到最新的 <code>state</code>，能不能用一个不变的值缓存 <code>state</code> ？ 等等？？ 不变的值？？？</p>
<h3 id="解决闭包问题最佳实践-usestate和useref">解决闭包问题最佳实践-<code>useState</code>和<code>useRef</code></h3>
<p><code>useRef</code>的返回是在整个组件生命周期都是不变的一个对象，可以借助 <code>useRef</code> 来获得最新的 <code>state</code>。例如这个例子可以改成这样：</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i34.23c65140M45Q5a"><code class="language-ts" style="white-space: pre;" data-spm-anchor-id="ata.21736010.0.i35.23c65140M45Q5a"><span>function Router() {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, </span><span style="color: rgb(0, 134, 179);">set</span><span>State] = useState</span><span style="color: rgb(0, 128, 128);">&lt;string&gt;</span><span>('');
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span data-spm-anchor-id="ata.21736010.0.i36.23c65140M45Q5a">Ref = useRef</span><span style="color: rgb(0, 128, 128);">&lt;string&gt;</span><span>(</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>);
</span><span>  // 这样，可以把 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>Ref 和最新的 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span> 绑定起来
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span data-spm-anchor-id="ata.21736010.0.i37.23c65140M45Q5a">Ref.current = </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>;
</span><span>  // 或者这样，可以把 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>Ref 和最新的 </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span> 绑定起来
</span>  useEffect(() =&gt; {
<span>    </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>Ref.current = </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>;
</span><span>  }, [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>]);
</span>  useEffect(() =&gt; {
<span>    </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> callback = () =&gt; {
</span><span>      </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span data-spm-anchor-id="ata.21736010.0.i44.23c65140M45Q5a"> latestState = </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>Ref.current;
</span>    };
<span>    window.addEventListener</span><span style="color: rgb(0, 128, 128);">&lt;'hashchange'&gt;</span><span>('hashchange', callback, false);
</span>  }, []);
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p data-spm-anchor-id="ata.21736010.0.i45.23c65140M45Q5a"><code>stateRef.current</code> 上面两种写法，都可以获得最新的 <code>count</code>，回调函数里面里面直接读取 <code>stateRef.current</code> 的值，可以拿到最新的 <code>state</code><br>闭包问题的最优解，节本就是这样了。</p>
<h3 id="useref-和-usestate-的最佳实践"><code>useRef</code> 和 <code>useState</code> 的最佳实践</h3>
<ul>
<li><code>useState</code> 和 <code>useRef</code> 仔细想想和和类组件的什么属相很相似？是不是和 <code>this.state</code> 和 <code>this</code> 的属性很像</li>
<li data-spm-anchor-id="ata.21736010.0.i38.23c65140M45Q5a">在类组件中，如果是不参渲染的属性，直接挂 <code>this</code> 上就好了，如果需要参与渲染的属性，挂在 <code>this.state</code> 上</li>
<li>同样的，在 <code data-spm-anchor-id="ata.21736010.0.i39.23c65140M45Q5a">Hook</code> 中，<code>useRef</code> 和 <code>useState</code> 可以实现类似效果</li>
</ul>
<p>例如以下的例子</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i41.23c65140M45Q5a"><code class="language-js" style="white-space: pre;"><span style="color: rgb(153, 153, 136); font-style: italic;">// 函数组件</span><span>
</span><span>const </span><span style="color: rgb(68, 85, 136); font-weight: bold;">Child</span><span> = </span><span style="color: rgb(68, 85, 136); font-weight: bold;">React</span><span>.memo(() =&gt; {
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">// count 参与页面渲染</span><span>
</span><span>  const [count, setCount] = useState(</span><span style="color: rgb(0, 128, 128);">0</span><span data-spm-anchor-id="ata.21736010.0.i40.23c65140M45Q5a">);
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">// userInfo 不参与渲染</span><span>
</span><span data-spm-anchor-id="ata.21736010.0.i42.23c65140M45Q5a">  const userInfo = useRef(</span><span style="color: rgb(0, 128, 128);">null</span><span>);
</span>});
<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 类组件</span><span>
</span><span></span><span class="hljs-class" style="color: rgb(51, 51, 51); font-weight: bold;">class</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">Child</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(51, 51, 51); font-weight: bold;">extends</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;" data-spm-anchor-id="ata.21736010.0.i43.23c65140M45Q5a">React</span><span class="hljs-class">.</span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">PureComponent</span><span class="hljs-class"> </span><span>{
</span>  constructor(props) {
<span>    </span><span style="color: rgb(51, 51, 51); font-weight: bold;">super</span><span>(props);
</span><span>    </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 不参与渲染</span><span>
</span><span>    </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.userInfo = </span><span style="color: rgb(0, 128, 128);">null</span><span>;
</span><span>    </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 参与渲染的属性</span><span>
</span><span>    </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.state = {
</span><span>      count: </span><span style="color: rgb(0, 128, 128);">0</span><span>,
</span>    };
  }
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="再看看-useeffect-回调函数的返回值">再看看 <code>useEffect</code> 回调函数的返回值</h3>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>type&nbsp;EffectCallback&nbsp;=&nbsp;</span><span class="hljs-function hljs-params">()</span><span class="hljs-function">&nbsp;=&gt;</span><span>&nbsp;(</span><span style="color: rgb(51, 51, 51); font-weight: bold;" data-spm-anchor-id="ata.21736010.0.i46.23c65140M45Q5a">void</span><span>&nbsp;|&nbsp;(</span><span class="hljs-function hljs-params">()</span><span class="hljs-function">&nbsp;=&gt;</span><span>&nbsp;</span><span style="color: rgb(51, 51, 51); font-weight: bold;">void</span><span>&nbsp;|&nbsp;</span><span style="color: rgb(0, 128, 128);">undefined</span><span>));
</span><span></span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">void</span><span>&nbsp;|&nbsp;(</span><span class="hljs-function hljs-params">()</span><span class="hljs-function">&nbsp;=&gt;</span><span>&nbsp;</span><span style="color: rgb(51, 51, 51); font-weight: bold;">void</span><span>&nbsp;|&nbsp;</span><span style="color: rgb(0, 128, 128);">undefined</span><span>)</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>确定是没有返回或者返回一个函数，所以下面这种写法是有问题的，虽然也没有明显标明返回体，就是没有返回一样，但是这个回调函数是异步函数，异步返回默认返回一个 <code>Promise</code> 对象，所以这种写法是不提倡的</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i47.23c65140M45Q5a"><code class="language-js" style="white-space: pre;"><span>const [data, setData] = useState({ hits: [] })</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  useEffect(</span><span style="color: rgb(0, 0, 128); font-weight: normal;" data-spm-anchor-id="ata.21736010.0.i53.23c65140M45Q5a">async</span><span> () =&gt; {
</span>    const result = await axios(
      'url‘,
<span>    )</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>    setData(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">result.data</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span data-spm-anchor-id="ata.21736010.0.i48.23c65140M45Q5a">}, [])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>为了规避这个问题，可以修改一下写法</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);" data-spm-anchor-id="ata.21736010.0.i52.23c65140M45Q5a"><code class="language-js" style="white-space: pre;"><span>useEffect(() =&gt; {
</span><span>  const </span><span>fetchData</span><span data-spm-anchor-id="ata.21736010.0.i50.23c65140M45Q5a"> = async () =&gt; {
</span><span>    const </span><span data-spm-anchor-id="ata.21736010.0.i55.23c65140M45Q5a">result</span><span> = await axios(</span><span style="color: rgb(221, 17, 68);">'url'</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span data-spm-anchor-id="ata.21736010.0.i51.23c65140M45Q5a">    setData(result.data)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }</span><span style="color: rgb(153, 153, 136); font-style: italic;" data-spm-anchor-id="ata.21736010.0.i49.23c65140M45Q5a">;</span><span>
</span><span data-spm-anchor-id="ata.21736010.0.i54.23c65140M45Q5a">  fetchData()</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>}, </span><span style="color: rgb(153, 0, 0); font-weight: bold;">[]</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="usecallback"><code>useCallback</code></h3>
<p data-spm-anchor-id="ata.21736010.0.i59.23c65140M45Q5a">把函数写进里面没什么问题，官方也推荐，但是万一我的副作用里面需要处理多个函数或者一个超长的函数的话，一个是不美观，一个是太难维护<br>这个适用可以利用 <code>useCallback</code> 把函数抽离出去，<code>useCallback</code> 返回一个记忆化的函数，当且仅当依赖列表有任何属性改变的时候，它才会返回一个新的函数，所以这个特性比较适合传给子组件的回调函数</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;" data-spm-anchor-id="ata.21736010.0.i56.23c65140M45Q5a"><span>function Counter() {
</span><span>  const [count, setCount] = useState(</span><span style="color: rgb(0, 128, 128);">0</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  const getFetchUrl = useCallback(() =&gt; {
    return 'https://v?query=' + count;
<span>  }, [count])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  useEffect(() =&gt; {
<span>    getFetchUrl()</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }, [getFetchUrl])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  return &lt;h1&gt;{count}&lt;/h1&gt;;
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>这里如果 <code>count</code> 改变的时候，<code>getFetchUrl</code>的值也会改变，从而导致 <code>useEffect</code> 也触发</p>
<h3 id="reactmemo" data-spm-anchor-id="ata.21736010.0.i58.23c65140M45Q5a"><code>React.memo</code></h3>
<p data-spm-anchor-id="ata.21736010.0.i57.23c65140M45Q5a"><code>React.memo()</code> 返回一个记忆化的值，如果 <code>React 内部会判定，如果重新渲染 </code>props` 不相等，就会重新渲染，如果没有改变，就不会触发组件渲染<br>这个特性比较有用，因为如果父组件重新渲染的时候，子组件就会重新渲染，使用这个特性可以减少不必要的子组件重新渲染</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> Child = memo(</span><span class="hljs-function">(</span><span class="hljs-function hljs-params">props</span><span class="hljs-function">) =&gt;</span><span> {
</span><span>  useEffect(</span><span class="hljs-function">() =&gt;</span><span> {
</span>  }, [])
<span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> (
</span><span>    </span><span style="color: rgb(153, 153, 136); font-style: italic;">// ...</span><span>
</span>  )
<span>}, </span><span class="hljs-function">(</span><span class="hljs-function hljs-params">prevProps, nextProps</span><span class="hljs-function">) =&gt;</span><span> {
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 判定相等的逻辑</span><span>
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 假如某些属性的改变不需要重新渲染</span><span>
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 可以编写这个函数</span><span>
</span>})
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="reactusecallback-和-reactmemo"><code>React.useCallback</code> 和 <code>React.memo</code></h3>
<ul>
<li><p>为什么讲 <code>useCallback</code> 要把 <code>memo</code> 拎出来讲，想一下 <code>useCallback</code> 的作用，返回一个缓存的函数，在函数组件里面，每次渲染都会执行一次组件函数，组件函数每次执行，在组件内部的函数都会重新定义，这样的话，父组件传给子组件的回调函数每次渲染都会变</p>
</li>
<li><p>再从 <code>memo</code> 的角度去看，父组件每次渲染，子函数组件如果不加 <code>memo</code> 的话，就算是子组件无任何依赖，属性都不变的情况下，子组件也会重新渲染</p>
</li>
<li><p>如果在父组件单独加为子组件的回调函数添加 <code>useCallback</code>，这样可以避免回调函数重新定义，但是子组件如果不用 <code>memo</code> 包裹，就算任何子组件属性没改变，还是会导致子组件重新渲染；</p>
</li>
<li><p>同样的，如果子组件单独用 <code>memo</code> 包裹，父组件每次渲染，重新定义回调函数，还是会导致重新</p>
</li>
<li><p>所以，<code>memo</code> 和 <code>useCallback</code> 必须都用上，不然是没用的，不仅达不到优化的效果，而且会加重 React 比较的负担。要不就别用，要不就都用上。</p>
</li>
</ul>
<h3 id="reactusecallback-和-reactmemo-最佳实践"><code>React.useCallback</code> 和 <code>React.memo</code> 最佳实践</h3>
<p>父组件用 <code>useCallback</code> 包裹函数，子组件用 <code>memo</code> 包裹组件，要不就都不用</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span style="color: rgb(153, 153, 136); font-style: italic;">// 子组件</span><span>
</span><span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// callback 为父组件传过来的回调函数</span><span>
</span><span></span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> Child = </span><span class="hljs-function">(</span><span class="hljs-function hljs-params">{ callback }</span><span class="hljs-function">) =&gt;</span><span> {}
</span><span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 子组件用 React.memo 包裹</span><span>
</span><span></span><span style="color: rgb(51, 51, 51); font-weight: bold;">export</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">default</span><span> React.memo(Child);
</span>
<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 父组件const Parent = () =&gt; {</span><span>
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 子组件的回调函数用 useCallback 包裹</span><span>
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> callback = React.useCallback(</span><span class="hljs-function">() =&gt;</span><span> {}, []);
</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">&lt;</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">Child</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;"> </span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">callback</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;">=</span><span class="xml" style="color: rgb(221, 17, 68); font-weight: normal;">{callback}</span><span class="xml" style="color: rgb(0, 0, 128); font-weight: normal;"> /&gt;</span><span>
</span>};
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="raectmemo-的局限"><code>Raect.memo</code> 的局限</h3>
<ul>
<li><p><code>React.memo</code> 包裹在组件上，可以对传给组件的属性进行判定，父组件导致子组件重新渲染的时候， <code>memo</code> 包裹的组件，会判定属性是否和上次渲染时候否改变，如果有改变，子组件重新渲染，否则不会重新渲染。</p>
</li>
<li><p><code>React.memo</code> 有个局限，只能防止来源于外部的属性，如果是来源于内部的属性，<code>React.memo</code> 是无作用的，例如通过 <code>useContext</code> 直接注入组件内部的属性，它没法防止，可以看下下面这个简单的例子</p>
</li>
</ul>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> Store = React.createContext(null);
</span><span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">default</span><span> function Parent() {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, dispatch] = useReducer(reducer, { count: </span><span style="color: rgb(0, 128, 128);">0</span><span>, step: </span><span style="color: rgb(0, 128, 128);">0</span><span> });
</span>
  return (
<span>    </span><span style="color: rgb(0, 128, 128);">&lt;Store.Provider value={{ dispatch, state }}&gt;</span><span>
</span><span>      </span><span style="color: rgb(0, 128, 128);">&lt;Step /&gt;</span><span>
</span><span>      </span><span style="color: rgb(0, 128, 128);">&lt;Count /&gt;</span><span>
</span>    &lt;/Store.Provider&gt;
  );
}

<span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> Count = memo(() =&gt; {
</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> { </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, dispatch } = useContext(Store);
</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> </span><span style="color: rgb(0, 134, 179);">set</span><span>Count = () =&gt; dispatch({ type: 'changeCount' });
</span> return (
<span> </span><span style="color: rgb(0, 128, 128);">&lt;&gt;</span><span>
</span><span> </span><span style="color: rgb(0, 128, 128);">&lt;span&gt;</span><span>count: {</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>.count}&lt;/span&gt;
</span><span> </span><span style="color: rgb(0, 128, 128);">&lt;button onClick={setCount}&gt;</span><span>change count&lt;/button&gt;
</span> &lt;/&gt;
);
});

<span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> Step = memo(() =&gt; {
</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> { </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, dispatch } = useContext(Store);
</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> </span><span style="color: rgb(0, 134, 179);">set</span><span>Count = () =&gt; dispatch({ type: 'changeStep' });
</span> return (
<span> </span><span style="color: rgb(0, 128, 128);">&lt;&gt;</span><span>
</span><span> </span><span style="color: rgb(0, 128, 128);">&lt;span&gt;</span><span>count: {</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>.step}&lt;/span&gt;
</span><span> </span><span style="color: rgb(0, 128, 128);">&lt;button onClick={setStep}&gt;</span><span>change step&lt;/button&gt;
</span> &lt;/&gt;
);
});
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>

<ul>
<li>上面的组件，<code>count</code> 或者 <code>step</code> 任意这个属性改变，都会导致两个子组件重新渲染，这显然是不对的。</li>
</ul>
<h3 id="reactusememo-代替-reactmomo"><code>React.useMemo</code> 代替 <code>React.momo</code></h3>
<p><code>useMemo</code> 和 <code>memo</code> 一样，返回一个记忆化的值，如果依赖项没有改变，会返回上一次渲染的结果，它和 <code>useCallback</code> 的差别就在一个是返回记忆化的函数，一个是返回记忆化的值，如果 <code>useMemo</code> 的回调函数执行返回一个函数，那它的效果和 <code>useCallback</code> 是一样的。<br>因而上面的组件可以改一下，下面这种写法就可以防止任意一个属性改变会导致两个子组件重新渲染的问题</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> Count = () =&gt; {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> { </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, dispatch } = useContext(Store);
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> </span><span style="color: rgb(0, 134, 179);">set</span><span>Count = () =&gt; dispatch({ type: 'changeCount' });
</span>  return useMemo(
    () =&gt; (
<span>      </span><span style="color: rgb(0, 128, 128);">&lt;&gt;</span><span>
</span><span>        </span><span style="color: rgb(0, 128, 128);">&lt;span&gt;</span><span>count: {</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>.count}&lt;/span&gt;
</span><span>        </span><span style="color: rgb(0, 128, 128);">&lt;button onClick={setCount}&gt;</span><span>change count&lt;/button&gt;
</span>      &lt;/&gt;
    ),
<span>    [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>.count]
</span>  );
};
<span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> Step = () =&gt; {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> { </span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>, dispatch } = useContext(Store);
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> </span><span style="color: rgb(0, 134, 179);">set</span><span>Step = () =&gt; dispatch({ type: 'changeStep' });
</span>  return useMemo(
    () =&gt; (
<span>      </span><span style="color: rgb(0, 128, 128);">&lt;&gt;</span><span>
</span><span>        </span><span style="color: rgb(0, 128, 128);">&lt;span&gt;</span><span>step: {</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>.step}&lt;/span&gt;
</span><span>        </span><span style="color: rgb(0, 128, 128);">&lt;button onClick={setStep}&gt;</span><span>change step&lt;/button&gt;
</span>      &lt;/&gt;
    ),
<span>    [</span><span style="color: rgb(51, 51, 51); font-weight: bold;">state</span><span>.step]
</span>  );
};
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="reactmomo-和-reactusememo"><code>React.momo</code> 和 <code>React.useMemo</code></h3>
<ul>
<li><code>React.momo</code> 在防止子组件重新渲染方面，是最简单的，在类组件里面有个 <code>React.PureComponent</code>，其作用也是。但是它无法检测函数内部的状态变化，并且防止重新渲染，例如 <code>useContext</code> 注入的状态。不过它自动比较全部属性，使用起来方面。</li>
<li><code>React.memo</code> 按照依赖列表是否有属性改变，决定是否返回新的值，一定程度上和 <code>Vue</code> 的计算属性类似，但是需要说动声明依赖的属性。相比 <code>React.momo</code>，它的控制的粒度更细，但是一般的外部属性变化，用这个明显没有 <code>React.memo</code> 方便</li>
</ul>
<h3 id="usereducer-usecontext"><code>useReducer</code> <code>useContext</code></h3>
<ul>
<li><code>useReducer</code> 是 <code>useState</code> 的一种替代方案，<code>useState</code> 的内部实现就是 <code>useReducer</code></li>
<li>它接收两个参数，和 <code>redux</code> 一样，一个是 <code>reducer</code>， 一个是初始值，有两个返回，一直是当前的 <code>state</code>，一个是 <code>dispatch</code></li>
<li>通过 <code>dispatch</code> 调用 <code>action</code> 就可以修改 <code>state</code> 里面的数据</li>
<li>本质的作用是，让数据和函数组件解耦，让函数组件只要发出 <code>Action</code>，就可以修改数据，由于数据不在组件内部，也不用处理内部 <code>state</code> 变化带来的 <code>effect</code>。</li>
<li><code>useContext</code> 和 <code>useReducer</code> 结合，一定程度上可以实现一个 <code>React Redux</code>，<a href="https://juejin.cn/post/6927530064867229703" target="_blank">掘金文章链接</a>，这个是之前的文章，这里不再展开</li>
</ul>
<h3 id="其他-hook">其他 <code>Hook</code></h3>
<ul>
<li><p><code>useImperativeHandle</code> ，搭配 <code>useRef</code> 和 <code>forwardRefs</code> 可以实现定制父组件可以引用子组件的属性和方法，而不是直接引用整个子组件的实例，在父组件需要调用子组件属性和方法，但是又不想全部属性和方法都给父组件调用的时候使用</p>
</li>
<li><p><code>useLayoutEffect</code> 使用的不多，作用和 <code>useEffect</code> 一样，但是这个 <code>hook</code> 是在组件变化后， <code>DOM</code> 节点生成后，渲染之前调用，区别于 <code>useEffect</code> 是渲染之后调用，不太推荐使用，会阻塞渲染</p>
</li>
<li><p><code>useDebugValue</code> 可用于在 <code>React</code> 开发者工具中显示自定义 <code>hook</code> 的标签。类似 <code>Vue</code> 组件用的 <code>name</code> 或者 <code>React</code> 组件中的 <code>displayName</code>，不影响代码运行</p>
</li>
</ul>
<h3 id="组件复用">组件复用</h3>
<p><code>React Hook</code> 有自定义 <code>Hook</code>，<code>React</code> 类组件有高阶组件或者渲染属性<br>有个比较常见的场景，进入页面需要调用后端接口的问题，如果每个组件都写一次，很繁琐，假设处理数据的接口长这样子</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-ts" style="white-space: pre;"><span style="color: rgb(51, 51, 51); font-weight: bold;">interface</span><span> </span><span style="color: rgb(153, 0, 115);">Response</span><span>&lt;</span><span style="color: rgb(153, 0, 115);">T</span><span>&gt; {
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">/** 是否有错误 */</span><span>
</span><span>  hasError: </span><span style="color: rgb(0, 134, 179);">bool</span><span>ean;
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">/** 是否有数据 */</span><span>
</span><span>  hasData: </span><span style="color: rgb(0, 134, 179);">bool</span><span>ean;
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">/** 是否请求中 */</span><span>
</span><span>  Loading: </span><span style="color: rgb(0, 134, 179);">bool</span><span>ean;
</span><span>  </span><span style="color: rgb(153, 153, 136); font-style: italic;">/** 请求回来的数据 */</span><span>
</span>  data: T;
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="高阶组件">高阶组件</h3>
<p>高阶组件<code>（HOC）</code>是 <code>React</code> 中用于复用组件逻辑的一种高级技巧。<code>HOC</code> 自身不是 <code>React API</code> 的一部分，它是一种基于 <code>React</code> 的组合特性而形成的设计模式。这种组件复用还挺常见的，比如 <code>React-redux</code> 里面的 <code>connect</code>，<code>React Router</code> 的 <code>withRouter</code></p>
<p>它可以做到：</p>
<ul>
<li>属性代理，比如多个组件都使用到的公共属性，注入属性</li>
<li>包裹组件，比如将组件包裹在写好的容器里面</li>
<li>渲染挟持，比如权限控制</li>
</ul>
<p>用处</p>
<ul>
<li>代码复用</li>
<li>性能监测 打点</li>
<li>权限控制，按照不懂的权限等级，渲染不同的页面</li>
</ul>
<h3 id="高阶组件编写和使用">高阶组件编写和使用</h3>
<p>按上面请求的需求，做一个组件渲染完之后，就立即开始请求初始数据</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>function requestWrapper(options) {
</span><span>  </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> (Component) =&gt; {
</span><span>    </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> </span><span class="hljs-class" style="color: rgb(51, 51, 51); font-weight: bold;">class</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">WapperComponent</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">extends</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">React</span><span class="hljs-class">.</span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">Component</span><span class="hljs-class"> </span><span>{
</span><span>      </span><span style="color: rgb(51, 51, 51); font-weight: bold;">constructor</span><span>(props) {
</span><span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">super</span><span>(props);
</span><span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.state = {
</span><span>          loading: </span><span style="color: rgb(0, 128, 128);">false</span><span>,
</span><span>          hasError: </span><span style="color: rgb(0, 128, 128);">false</span><span>,
</span><span>          hasData: </span><span style="color: rgb(0, 128, 128);">false</span><span>,
</span><span>          </span><span style="color: rgb(51, 51, 51); font-weight: bold;">data</span><span>: </span><span style="color: rgb(0, 128, 128);">null</span><span>,
</span>        };
      }
      httpRequest = async () =&gt; {
<span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.setState({ loading: </span><span style="color: rgb(0, 128, 128);">true</span><span> });
</span><span>        </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 这里做一些请求工作，我这里就不写了，没必要</span><span>
</span><span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.setState({ hasData: </span><span style="color: rgb(0, 128, 128);">true</span><span> });
</span><span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.setState({ hasError: </span><span style="color: rgb(0, 128, 128);">false</span><span> });
</span><span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.setState({
</span><span>          </span><span style="color: rgb(51, 51, 51); font-weight: bold;">data</span><span>: {
</span><span>            </span><span style="color: rgb(153, 153, 136); font-style: italic;">/** 这里是请求回来的数据 */</span><span>
</span>          },
        });
<span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.setState({ loading: </span><span style="color: rgb(0, 128, 128);">false</span><span> });
</span>      };
      componentDidMount() {
<span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.httpRequest();
</span>      }
      render() {
<span>        </span><span style="color: rgb(153, 153, 136); font-style: italic;">// 透传外部传过来的属性，然后合并 this.state，传给包裹组件</span><span>
</span><span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">const</span><span> combineProps = { ...</span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.props, ...</span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.state };
</span><span>        </span><span style="color: rgb(51, 51, 51); font-weight: bold;">return</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">this</span><span>.state.loading ? (
</span>          &lt;Loading /&gt;
        ) : (
          &lt;Component {...combineProps} /&gt;
        );
      }
    };
  };
}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>使用方面，高阶组件可以修饰类组件或者函数组件</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>function </span><span style="color: rgb(68, 85, 136); font-weight: bold;">Page</span><span>(props) {
</span><span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// props 包含 loading hasError hasData data prop1</span><span>
</span><span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 其中 prop1 来源于外部属性，其他的属性来源于包裹的组件</span><span>
</span>}
<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 类组件使用，使用装饰器</span><span>
</span><span></span><span style="color: rgb(153, 153, 153); font-weight: bold;">@requestWrapper</span><span>({url: '', param: {} })
</span><span></span><span class="hljs-class" style="color: rgb(51, 51, 51); font-weight: bold;">class</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">ClassComponent</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(51, 51, 51); font-weight: bold;">extends</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">React</span><span class="hljs-class">.</span><span class="hljs-class" style="color: rgb(153, 0, 0); font-weight: bold;">PureComponent</span><span class="hljs-class"> </span><span>{
</span>}
<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 类组件使用，不适用装饰器</span><span>
</span><span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">default</span><span> requestWrapper({url: '', param: {} })(</span><span style="color: rgb(68, 85, 136); font-weight: bold;">ClassComponent</span><span>);
</span><span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 函数式组件使用</span><span>
</span><span>const </span><span style="color: rgb(68, 85, 136); font-weight: bold;">WrapPage</span><span> = requestWrapper({ url: '', param: {} })(</span><span style="color: rgb(68, 85, 136); font-weight: bold;">Page</span><span>);
</span><span>export </span><span style="color: rgb(51, 51, 51); font-weight: bold;">default</span><span> </span><span style="color: rgb(68, 85, 136); font-weight: bold;">WrapPage</span><span>;
</span><span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 使用</span><span>
</span><span>&lt;</span><span style="color: rgb(68, 85, 136); font-weight: bold;">WrapPage</span><span> prop1=</span><span style="color: rgb(221, 17, 68);">"1"</span><span> /&gt;;</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="自定义-hook-的编写和使用">自定义 <code>Hook</code> 的编写和使用</h3>
<p>自定义 <code>Hook</code> 的编写，一个简单的数据请求的 <code>Hook</code></p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>function useRequest(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">options</span><span>) {
</span><span>  const [loading, setLoading] = useState(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">false</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  const [hasError, setHasError] = useState(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">false</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  const [hasData, setHasData] = useState(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">false</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  const [data, setData] = useState(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">null</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>  useEffect(() =&gt; {
    async function reqeust() {
<span>      setLoading(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">true</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>      /** 这里依旧是请求，没写 */
<span>      setHasError(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">false</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>      setHasData(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">true</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>      setData({
        /** 请求回来的数据 */
<span>      })</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>      setLoading(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">false</span><span>)</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>    }
<span>    reqeust()</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  }, [])</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span><span>  return { loading, hasError, hasData, data }</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
</code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<p>自定义 <code>hook</code> 只能在函数式组件使用，不能在类组件里面用</p>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span>function Page(</span><span style="color: rgb(0, 0, 128); font-weight: normal;">props</span><span>) {
</span>  // 这次的 props 只有 prop1 这个属性
  const { loading, hasError, hasData, data } = useRequest({
    url: ‘’,
    param: {},
<span>  })</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span><span>
</span>}
<span>&lt;Page prop</span><span style="color: rgb(0, 128, 128);">1</span><span>={</span><span style="color: rgb(0, 128, 128);">1</span><span>} /&gt;</span><span style="color: rgb(153, 153, 136); font-style: italic;">;</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>
<h3 id="函数式式组件和类组件默认属性">函数式式组件和类组件默认属性</h3>
<div class="syntax-highlighter_3YnAN"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(51, 51, 51); background: rgb(248, 248, 248);"><code class="language-js" style="white-space: pre;"><span style="color: rgb(51, 51, 51); font-weight: bold;">class</span><span> Button extends React.PureComponent {
</span><span>  static defaultProps = { </span><span style="color: rgb(51, 51, 51); font-weight: bold;">type</span><span>: </span><span style="color: rgb(221, 17, 68);">"primary"</span><span>, onChange:</span><span class="hljs-function"> </span><span class="hljs-function hljs-params">()</span><span class="hljs-function"> =&gt;</span><span> {} };
</span>}

<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 不论是函数式还是类都可以这么玩，这也是类静态属性的另外一种写法</span><span>
</span><span></span><span class="hljs-module-access hljs-module hljs-identifier">Button</span><span class="hljs-module-access hljs-module">.</span><span>defaultProps = {
</span><span> </span><span style="color: rgb(51, 51, 51); font-weight: bold;">type</span><span>: </span><span style="color: rgb(221, 17, 68);">"primary"</span><span>,
</span><span> onChange:</span><span class="hljs-function"> </span><span class="hljs-function hljs-params">()</span><span class="hljs-function"> =&gt;</span><span> {}
</span>};

<span></span><span style="color: rgb(51, 51, 51); font-weight: bold;">function</span><span> </span><span class="hljs-constructor">Button({ </span><span class="hljs-constructor hljs-params">type</span><span class="hljs-constructor">, </span><span class="hljs-constructor hljs-params">onChange</span><span class="hljs-constructor"> })</span><span> {}
</span>
<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 这样写看起来没问题，但是实际上，如果父组件没传 onChange，onChange</span><span>
</span><span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 每次组件渲染都会生成一个新的函数，引用类型都有这个问题</span><span>
</span><span></span><span style="color: rgb(51, 51, 51); font-weight: bold;">function</span><span> </span><span class="hljs-constructor">Button({ </span><span class="hljs-constructor hljs-params">type</span><span class="hljs-constructor"> = </span><span class="hljs-constructor" style="color: rgb(221, 17, 68);">"primary"</span><span class="hljs-constructor">, </span><span class="hljs-constructor hljs-params">onChange</span><span class="hljs-constructor"> = ()</span><span> =&gt; {} }) {}
</span>
<span></span><span style="color: rgb(153, 153, 136); font-style: italic;">// 这很 OK，你可真是个小机灵鬼</span><span>
</span><span>const changeMet =</span><span class="hljs-function"> </span><span class="hljs-function hljs-params">()</span><span class="hljs-function"> =&gt;</span><span> {}
</span><span></span><span style="color: rgb(51, 51, 51); font-weight: bold;">function</span><span> </span><span class="hljs-constructor">Button({ </span><span class="hljs-constructor hljs-params">type</span><span class="hljs-constructor"> = “</span><span class="hljs-constructor hljs-params">primary</span><span class="hljs-constructor">”, </span><span class="hljs-constructor hljs-params">onChange</span><span class="hljs-constructor"> = </span><span class="hljs-constructor hljs-params">changeMet</span><span class="hljs-constructor"> })</span><span> {}</span></code></pre><div class="syntax-highlighter-copy_1eBR0"> 复制</div></div>

<h3 id="类组件的问题被解决了么？">类组件的问题被解决了么？</h3>
<p>复用组件状态逻辑难</p>
<ul>
<li>依赖自定义的 Hook，可以解决组件状态和逻辑复用的问题，但是自定义 <code>Hook</code> 编写需要对 <code>Hook</code> 运行机制非常了解，门槛并不比高阶组件低</li>
</ul>
<p>生命周期带来的负面影响，逻辑拆分严重</p>
<ul>
<li>生命周期拆分逻辑的问题，在 <code>Hook</code> 里面切实被解决了，不会存在同一个逻辑被拆分在 <code>N</code> 个生命周期里面了</li>
</ul>
<p><code>This</code> 的指向问题</p>
<ul>
<li>这个问题在 Hook 里面也是解决了，因为函数没有 <code>this</code>，就不会有 <code>this</code> 的问题，但是相对的，如果需要一个不变的对象，请使用 <code>useRef</code></li>
</ul>
<h3 id="简单总结">简单总结</h3>
<ul>
<li><p><code>useState</code>可以实现类似 <code>state</code> 和 <code>setState</code> 的效果</p>
</li>
<li><p><code>useEffect</code> 可以实现 <code>componentDidMount</code> <code>componentDidUpdate</code> <code>componentWillUnmount</code> 这几个生命周期的功能，并且写法更加简单，在每次渲染后都会触发，触发的条件是依赖项有改变</p>
</li>
<li><p><code>useRef</code> 返回一个引用，每次渲染都返回同一个对象，和类组件 <code>this</code> 属性一致</p>
</li>
<li><p><code>useCallback</code> 返回一个记忆化的回调函数，在依赖项改变的时候，回调函数会修改，否则返回之前的回调函数，对于一些需要传给子组件的函数，可以使用这个，避免子组件因为回调函数改变而改变</p>
</li>
<li><p><code>useMemo</code> 返回一个记忆化的值，依赖项改变，返回的值才会变，可用来记忆化值，和 <code>Vue</code> 计算属性类似，避免重复计算，避免重复渲染</p>
</li>
<li><p>自定义的<code>Hook</code>是实现状态和逻辑复用，作用和高阶组件还有渲染属性差不多</p>
</li>
<li><p><code>useReducer</code> 是 <code>useState</code> 的底层实现，可以管理多个 <code>state</code>，把 <code>state</code> 从组件内部抽离出来</p>
</li>
<li><p><code>useContext</code> 可以实现批量传值，注入多个组件，和 <code>useReducer</code> <code>useMemo</code> 使用可以实现 <code>Redux</code> 的功能</p>
</li>
</ul>
<h2 id="使用感受">使用感受</h2>
<h3 id="个人使用方面">个人使用方面</h3>
<ul>
<li><p>函数式组件本身写起来就比类组件少写不少代码</p>
</li>
<li><p>闭包问题很影响开发和调试，提高了不少调试成本，如果不熟悉闭包机制，很难发现问题。<code>Hook</code> 中的闭包问题，大多还是由于依赖项没有填写导致</p>
</li>
<li><p>闭包带来的问题，比类组件 <code>This</code> 的更加恼人，主要调试不好发现问题，填不填依赖项也是一个让人纠结的活</p>
</li>
<li><p><code>Hook</code> 的依赖不能自动识别，必须手动声明，虽然有插件辅助添加，但是使用起来还是不如 <code>Vue</code> 的 <code>Hook</code></p>
</li>
<li><p>在熟悉 <code>Hook</code> 的机制的情况下，<code>Hook</code> 开发体验还是比类组件好很多</p>
</li>
</ul>
<h3 id="团队协作方面">团队协作方面</h3>
<ul>
<li>其实在推广 <code>Hook</code> 的时候，团队成员的 <code>Hook</code> 水平是不太一致的，很多人员就遇到了闭包问题，还有依赖死循环的问题，这个可能大大小小都遇到过，就好像上面提到的，解决闭包问题，方式五花八门，其实也是我自己摸索过来的，然后看到团队成员其实差不多还使用者 <code>state</code> 更新之后，重新设置监听的方式，这个并不是太好，只能说闭包问题解决了</li>
<li>相对的，<code>React</code> 官方也没有总结太多最佳实践，很多都靠自己实践过来的，所以团队成员在刚接触 <code>Hook</code> 的时候，都是 <code>useEffect</code> <code>useState</code> 两把 <code>API</code>，甚至在 <code>React Hook</code> 的官方文档里面 <a href="https://react.docschina.org/docs/hooks-intro.html" target="_blank">Hook 简介</a>，对于这两个 <code>Hook</code> 介绍的很多</li>
<li>但对于其他常用的 <code>Hook</code>，比如 <code>useRef</code> 和 <code>useCallback</code> 使用场景其实没有太好的例子去支撑这些 <code>API</code> 的使用。倒是其实团队里面不少成员，面对着不参与渲染的属性，也是用 <code>useState</code> ，而不是使用 <code>useRef</code>。就是很多新人接触 <code>Hook</code> 容易犯的一个错误。</li>
<li>有不少同学有些插件没有装上，导致 <code>React</code> 自动检测依赖项的插件没有生效，这无疑会给本身就难以发现的闭包问题加了一层霜</li>
<li>所以我也定期在团队里面分享我认为是比较好的实践，去引导团队里面的同学</li>
<li data-spm-anchor-id="ata.21736010.0.i64.23c65140M45Q5a">对于不喜欢用 <code data-spm-anchor-id="ata.21736010.0.i65.23c65140M45Q5a">React Hook</code> 的同学，直接用类组件，类组件虽然代码写起来繁琐，但是起码没有闭包这些问题，而且代码被接手之后容易读懂，<code>React Hook</code> 只是一个工具，会使用会给你加分，但是不会使用只会用类组件，也不会对其他人代码有影响，比较类组件和函数组件是可以共存的</li>
</ul>
`
