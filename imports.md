<h1><a name="imports">World imports</a></h1>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#wasi:i2c_i2c_0.2.0_draft"><code>wasi:i2c/i2c@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:i2c_delay_0.2.0_draft"><code>wasi:i2c/delay@0.2.0-draft</code></a></li>
</ul>
</li>
</ul>
<h2><a name="wasi:i2c_i2c_0.2.0_draft"></a>Import interface wasi:i2c/i2c@0.2.0-draft</h2>
<p>Inter-Integrated Circuit (I²C) API that is based upon <a href="https://github.com/sunfishcode/hello-embedded/tree/main">hello-embedded</a> and <a href="https://github.com/rust-embedded/embedded-hal">embedded-hal</a>.</p>
<hr />
<h3>Types</h3>
<h4><a name="address"></a><code>type address</code></h4>
<p><code>u16</code></p>
<p>An address value, in either 7-bit or 10-bit form, depending on the device.
<h4><a name="no_acknowledge_source"></a><code>enum no-acknowledge-source</code></h4>
<p>No-acknowledge error source.</p>
<p>In cases where it is possible, a device should indicate if a no
acknowledge response was received to an address versus a no acknowledge
to a data byte. Where it is not possible to differentiate, Unknown
should be indicated.</p>
<h5>Enum Cases</h5>
<ul>
<li>
<p><a name="no_acknowledge_source.address"></a><a href="#address"><code>address</code></a></p>
<p>The device did not acknowledge its address. The device may be
missing.
</li>
<li>
<p><a name="no_acknowledge_source.data"></a><code>data</code></p>
<p>The device did not acknowledge the data. It may not be ready to
process requests at the moment.
</li>
<li>
<p><a name="no_acknowledge_source.unknown"></a><code>unknown</code></p>
<p>Either the device did not acknowledge its address or the data, but
it is unknown which.
</li>
</ul>
<h4><a name="error_code"></a><code>variant error-code</code></h4>
<p>Operation errors.</p>
<h5>Variant Cases</h5>
<ul>
<li>
<p><a name="error_code.bus"></a><code>bus</code></p>
<p>Bus error occurred. e.g. A START or a STOP condition is detected and
is not located after a multiple of 9 SCL clock pulses.
</li>
<li>
<p><a name="error_code.arbitration_loss"></a><code>arbitration-loss</code></p>
<p>The arbitration was lost, e.g. electrical problems with the clock signal.
</li>
<li>
<p><a name="error_code.no_acknowledge"></a><code>no-acknowledge</code>: <a href="#no_acknowledge_source"><a href="#no_acknowledge_source"><code>no-acknowledge-source</code></a></a></p>
<p>A bus operation was not acknowledged, e.g. due to the addressed
device not being available on the bus or the device not being ready
to process requests at the moment.
</li>
<li>
<p><a name="error_code.overrun"></a><code>overrun</code></p>
<p>The peripheral receive buffer was overrun.
</li>
<li>
<p><a name="error_code.other"></a><code>other</code></p>
<p>A different error occurred.
</li>
</ul>
<h4><a name="operation"></a><code>variant operation</code></h4>
<p>An operation used by the <code>transaction</code> method.</p>
<h5>Variant Cases</h5>
<ul>
<li>
<p><a name="operation.read"></a><code>read</code>: <code>u64</code></p>
<p>Read the give number of bytes.
</li>
<li>
<p><a name="operation.write"></a><code>write</code>: list&lt;<code>u8</code>&gt;</p>
<p>Write the given bytes.
</li>
</ul>
<h4><a name="i2c"></a><code>resource i2c</code></h4>
<hr />
<h3>Functions</h3>
<h4><a name="method_i2c.transaction"></a><code>[method]i2c.transaction: func</code></h4>
<p>Execute the provided <a href="#operation"><code>operation</code></a>s on the I²C bus.</p>
<h5>Params</h5>
<ul>
<li><a name="method_i2c.transaction.self"></a><code>self</code>: borrow&lt;<a href="#i2c"><a href="#i2c"><code>i2c</code></a></a>&gt;</li>
<li><a name="method_i2c.transaction.address"></a><a href="#address"><code>address</code></a>: <a href="#address"><a href="#address"><code>address</code></a></a></li>
<li><a name="method_i2c.transaction.operations"></a><code>operations</code>: list&lt;<a href="#operation"><a href="#operation"><code>operation</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_i2c.transaction.0"></a> result&lt;list&lt;list&lt;<code>u8</code>&gt;&gt;, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h4><a name="method_i2c.read"></a><code>[method]i2c.read: func</code></h4>
<p>Reads <code>len</code> bytes from address <a href="#address"><code>address</code></a>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_i2c.read.self"></a><code>self</code>: borrow&lt;<a href="#i2c"><a href="#i2c"><code>i2c</code></a></a>&gt;</li>
<li><a name="method_i2c.read.address"></a><a href="#address"><code>address</code></a>: <a href="#address"><a href="#address"><code>address</code></a></a></li>
<li><a name="method_i2c.read.len"></a><code>len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_i2c.read.0"></a> result&lt;list&lt;<code>u8</code>&gt;, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h4><a name="method_i2c.write"></a><code>[method]i2c.write: func</code></h4>
<p>Writes bytes to target with address <a href="#address"><code>address</code></a>.</p>
<h5>Params</h5>
<ul>
<li><a name="method_i2c.write.self"></a><code>self</code>: borrow&lt;<a href="#i2c"><a href="#i2c"><code>i2c</code></a></a>&gt;</li>
<li><a name="method_i2c.write.address"></a><a href="#address"><code>address</code></a>: <a href="#address"><a href="#address"><code>address</code></a></a></li>
<li><a name="method_i2c.write.data"></a><code>data</code>: list&lt;<code>u8</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_i2c.write.0"></a> result&lt;_, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h4><a name="method_i2c.write_read"></a><code>[method]i2c.write-read: func</code></h4>
<p>Writes bytes to address <a href="#address"><code>address</code></a> and then reads <code>read-len</code> bytes
in a single transaction.</p>
<h5>Params</h5>
<ul>
<li><a name="method_i2c.write_read.self"></a><code>self</code>: borrow&lt;<a href="#i2c"><a href="#i2c"><code>i2c</code></a></a>&gt;</li>
<li><a name="method_i2c.write_read.address"></a><a href="#address"><code>address</code></a>: <a href="#address"><a href="#address"><code>address</code></a></a></li>
<li><a name="method_i2c.write_read.write"></a><code>write</code>: list&lt;<code>u8</code>&gt;</li>
<li><a name="method_i2c.write_read.read_len"></a><code>read-len</code>: <code>u64</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_i2c.write_read.0"></a> result&lt;list&lt;<code>u8</code>&gt;, <a href="#error_code"><a href="#error_code"><code>error-code</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi:i2c_delay_0.2.0_draft"></a>Import interface wasi:i2c/delay@0.2.0-draft</h2>
<p>Delays.</p>
<hr />
<h3>Types</h3>
<h4><a name="delay"></a><code>resource delay</code></h4>
<h2>Delay with up to nanosecond precision.</h2>
<h3>Functions</h3>
<h4><a name="method_delay.delay_ns"></a><code>[method]delay.delay-ns: func</code></h4>
<p>Pauses execution for at minimum <code>ns</code> nanoseconds. Pause can be
longer if the implementation requires it due to precision/timing
issues.</p>
<h5>Params</h5>
<ul>
<li><a name="method_delay.delay_ns.self"></a><code>self</code>: borrow&lt;<a href="#delay"><a href="#delay"><code>delay</code></a></a>&gt;</li>
<li><a name="method_delay.delay_ns.ns"></a><code>ns</code>: <code>u32</code></li>
</ul>
