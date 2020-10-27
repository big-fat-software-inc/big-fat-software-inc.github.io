# Memory Usage in Web Sites

## Inspiration

I have two low end portable computers lying around at my home. The ones with higher specs are all desktops. Plus, I'm not very fond of mobile devices because they're seldom useful for productive work. They're useful only for content consumption & low-effort content upload.

Chrome is very famous for leaving all fans buzzing on computers whenever it launches. It's very easy to pass the blame to the browser or the browser vendor. But as a web programmer, my objective is to look at other possibilities - like, whether is it possible indeed to 



## Load Testing

```js
(() => {
 let x = [];
 for( let i = 0; i < 10000000; ++i ) {
  x.push(btoa(unescape(encodeURIComponent(window.location.href))));
 }
})();
```

The snippet above loops 10 million times and inserts the Base64 encoded URL of the page into the browser's memory. Will this snippet crash your system? Well, that's hard to say. But that isn't the important question. The real question is, how do we set memory quotas for a website and prevent a website from exceeding its quota.

And, if for some reason, it reaches the peak, we must devise some mechanism to sacrifice some part of the site to stay within the memory budget. 

## Good Ol' Days

In the old internet explorer days, it was possible to *force the garbage collector to run immediately* and release memory by calling [an undocumented `CollectGarbage` method](http://ajaxian.com/archives/heap-feng-shui-in-javascript-and-heaplib). This was part of the ***JScript*** specification.

### Reference Counting

The old garbage collectors relied on the method of ***Reference Counting***. Therefore, consciously ***setting all reference-storing variables to* `null`**  was the go-to method.

Reference-storing-variables are those which store reference to composite types like Arrays and Objects, functions, or may be an instance of the DOM element or a collection of DOM elements.









### Sample Load Testing Snippet

#### `now` method

The `now` method returns a [`DOMHighResTimeStamp`](https://www.w3.org/TR/hr-time-1/#sec-DOMHighResTimeStamp) representing the number of milliseconds from the [`navigationStart`](http://www.w3.org/TR/navigation-timing/#dom-performancetiming-navigationstart) attribute of the [`PerformanceTiming`](http://www.w3.org/TR/navigation-timing/#performancetiming) interface [[NavigationTiming\]](https://www.w3.org/TR/hr-time-1/#NavigationTiming), the start of navigation of the document, to the occurrence of the call to the [`now`](https://www.w3.org/TR/hr-time-1/#dom-performance-now) method.

```js
>> window.performance.now()
<< 1363450.0800000387
```

The [`DOMHighResTimeStamp`](https://www.w3.org/TR/hr-time-1/#sec-DOMHighResTimeStamp) differs from the usual time stamp in the following manner:

```js
>> window.performance.now()
<< 1509874.7300000396

>> +Date.now()
<< 1603740310921
```







```js
>> window.performance.memory
<< MemoryInfo {totalJSHeapSize: 14779462, usedJSHeapSize: 10350254, jsHeapSizeLimit: 4294705152}
jsHeapSizeLimit: 4294705152
totalJSHeapSize: 14779462
usedJSHeapSize: 10350254
```



```js
>> window.performance.eventCounts
<< EventCounts {size: 36}

```

##### Specification

https://www.w3.org/TR/hr-time-1/#performance



### Sample Load Testing Snippet

```js
(() => {
 let x = [];

 for( let i = 0; i < 10000000; ++i ) {
  x.push(btoa(unescape(encodeURIComponent(window.location.href))));
 }

 alert('deleting');   // <--- memory usage around 500mb
 delete x;            // <--- immediate results in Firefox 3.5 (not IE8)
 alert('done');
})();
```



