# Nginx-is-start-gzip-Compression-contrast
nginx开启gzip压缩的配置详解和压缩效果对比


<h3 style="box-sizing: border-box; font-family: &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-weight: normal; line-height: 1.1; color: rgb(51, 51, 51); margin-top: 0px; margin-bottom: 10px; font-size: 24px; white-space: normal; background-color: rgb(238, 238, 238); text-align: justify;">
    <span style="box-sizing: border-box; font-size: 16px;">简单介绍一下</span>
</h3>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 15px; font-size: 15px; color: rgb(85, 85, 85); font-family: Georgia, &quot;Times New Roman&quot;, Times, serif; white-space: normal; background-color: rgb(238, 238, 238);">
    <span style="box-sizing: border-box; font-size: 14px;">&nbsp;&nbsp;&nbsp;&nbsp;<span style="box-sizing: border-box;">开启nginx gzip压缩后，html、css、js等静态资源的大小会大大的减少，从而可以节约大量的带宽，提高传输效率，用户浏览网站会跟加快速。但会消耗cpu资源（当然了具体看你服务器配置啦），但是为了给用户更好的体验这些都不算什么滴。</span></span>
</p>
<h3 style="box-sizing: border-box; font-family: &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-weight: normal; line-height: 1.1; color: rgb(51, 51, 51); margin-top: 0px; margin-bottom: 10px; font-size: 24px; white-space: normal; background-color: rgb(238, 238, 238); text-align: justify;">
    <span style="box-sizing: border-box; font-size: 16px;">一、配置和解析</span>
</h3>
<pre class="brush:bash;toolbar:false" style="box-sizing: border-box; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; padding: 9.5px; margin-top: 0px; margin-bottom: 10px; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">http{
    # nginx.conf 找到对应的行跟改下列配置 
    gzip on;                #开启或者关闭gzip模块    
    gzip_min_length 1k;     #不压缩临界值，大于1K的才压缩，一般不用改
    gzip_disable &quot;msie6&quot;;   #IE6对Gzip不怎么友好，不给它Gzip了   
    # gzip_vary on;
    # gzip_proxied any;
    gzip_comp_level 6;           #gzip压缩比，1 压缩比最小处理速度最快，9 压缩比最大但处理最慢（传输快但比较消耗cpu）。
    gzip_buffers 16 8k;           #设置系统获取几个单位的缓存用于存储gzip的压缩结果数据流。
    # gzip_http_version 1.1;   #识别http的协议版本,99.99%的浏览器基本上都支持gzip解压了，所以可以不用设这个值,保持系统默认即可。
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;            #如果你希望压缩常规的文件类型,（无论是否指定）&quot;text/html&quot;类型总是会被压缩的。
 }</pre>
<h3 style="box-sizing: border-box; font-family: &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-weight: normal; line-height: 1.1; color: rgb(51, 51, 51); margin-top: 0px; margin-bottom: 10px; font-size: 24px; white-space: normal; background-color: rgb(238, 238, 238); text-align: justify;">
    <span style="box-sizing: border-box; font-size: 16px;"></span>
</h3>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 15px; font-size: 15px; color: rgb(85, 85, 85); font-family: Georgia, &quot;Times New Roman&quot;, Times, serif; white-space: normal; background-color: rgb(238, 238, 238);">
    <span style="box-sizing: border-box; color: rgb(0, 176, 80); font-size: 14px;">&nbsp;&nbsp;&nbsp;&nbsp;PS：千万别忘记重启服务</span>
</p>
<h3 style="box-sizing: border-box; font-family: &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-weight: normal; line-height: 1.1; color: rgb(51, 51, 51); margin-top: 0px; margin-bottom: 10px; font-size: 24px; white-space: normal; background-color: rgb(238, 238, 238); text-align: justify;">
    <span style="box-sizing: border-box; font-size: 16px;">二、检查是否开启</span>
</h3>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 15px; font-size: 15px; color: rgb(85, 85, 85); font-family: Georgia, &quot;Times New Roman&quot;, Times, serif; white-space: normal; background-color: rgb(238, 238, 238);">
    &nbsp; &nbsp;&nbsp;<img src="http://www.piaoyifa.com/uploads/image/1519568157121826.png" title="1519568157121826.png" alt="1517283856112514.png" class="img-responsive"/>
</p>
<h3 style="box-sizing: border-box; font-family: &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif; font-weight: normal; line-height: 1.1; color: rgb(51, 51, 51); margin-top: 0px; margin-bottom: 10px; font-size: 24px; white-space: normal; background-color: rgb(238, 238, 238); text-align: justify;">
    <span style="box-sizing: border-box; font-size: 16px;">三、对比前后效果（我只能说是效果显著）</span>
</h3>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 15px; font-size: 15px; color: rgb(85, 85, 85); font-family: Georgia, &quot;Times New Roman&quot;, Times, serif; white-space: normal; background-color: rgb(238, 238, 238);">
    <span style="box-sizing: border-box; font-size: 16px;"><img src="http://www.piaoyifa.com/uploads/image/1519568180776249.png" title="1519568180776249.png" alt="1517284029102786.png" class="img-responsive"/></span>
</p>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 15px; font-size: 15px; color: rgb(85, 85, 85); font-family: Georgia, &quot;Times New Roman&quot;, Times, serif; white-space: normal; background-color: rgb(238, 238, 238);">
    <img src="http://www.piaoyifa.com/uploads/image/1519568204949291.png" title="1519568204949291.png" alt="1517284080429928.png" class="img-responsive"/>
</p>
<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 15px; font-size: 15px; color: rgb(85, 85, 85); font-family: Georgia, &quot;Times New Roman&quot;, Times, serif; white-space: normal; background-color: rgb(238, 238, 238);">
    <span style="box-sizing: border-box; font-size: 14px;">&nbsp;惊不惊喜？意不意外？嘿嘿。。。</span>
</p>
<p>
    <br/>
</p>
