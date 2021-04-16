---
layout: post
title:  "[Algorithm] Quick Sort"
subtitle:   "quicksort"
categories: develop
tags: algorithm
comments: true
---

# 퀵정렬
---

## 퀵정렬 알고리즘
---
1. 적당한 값 p를 고른다. p값을 고를 때는 가능한 그 값의 크기가 p값 이상인 요소의 개수와 p값 이하인 요소의 개수가 같도록 한다.
2. 배열 앞부분에는 p 값 이상인 요소를 옮기고, 배열 뒷부분에는 p 값 이하인 요소를 옮긴다.
3. 배열 앞부분에는 길이가 2 이상이면 그 부분을 대상으로 퀵 정렬을 한다.
4. 배열 뒷부분의 길이가 2 이상이면 그 부분을 대상으로 퀵 정렬을 한다.

## javascript 코드를
---
```javascript
    function quicksort(x, first, last) {
        var p = x[ Math.floor((first+last)/2)];
        for(var i=first, j=last; ; i++, j--) {
            while(x[i]<p) i++;
            while(p<x[j]) j--;
            if(i>=j) break;
            var w = x[i]; x[i] = x[j]; x[j] = w;
        }
        if(first < i-1) quicksort(x, first, i-1);
        if(j+1<last) quicksort(x, j+1, last);
    }
    var a = [7, 2, 5, 1, 8, 9, 3];
    quicksort(a, 0, a.length-1);
    console.log(a); // -> [1,2,3,4,5,6,7,8,9]
```