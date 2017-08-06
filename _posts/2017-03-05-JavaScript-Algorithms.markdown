---
layout:     post
title:      JS常用排序算法总结
date:       2017-03-05
tags:
    - JavaScript
---	

1、插入排序

    思想：构建有序数列，对于未排序的数据，在已排序的数据中从后向前找到合适的位置插入直到未排序的数据个数为0（时间复杂度为n^2）；（注意：在已排序的中找到合适的位置可以采用二分查找提高效率，这样最后的时间复杂度为n^2）。

    代码：
        function insertSort(array){
            var i,j,temp,low,mid,high,result,len = array.length;
            if(len <= 1) return array;
            result = array.slice(0);
            for(i = 1;i < len;i++){
                temp = result[i];
                low = 0;
                high = i - 1;
                while(low <= high){
                    mid = parseInt((low+high)/2, 10);
                    if(temp < result[mid]) high = mid - 1;
                    else low = mid + 1;
                }
                for(j = i - 1;j >= high + 1;j--){
                    result[j+1] = result[j];
                }
                result[j+1] = temp;
            }
            return result;
        }
        insertSort([1,3,55,4,77]);  //[1, 3, 4, 55, 77]

2、冒泡排序

    思想：相邻两元素进行比较，若前一个元素大于后一个元素，则交换顺序，这一轮会找出最大或者最小的元素；然后在剩下的元素重复上述操作直至所有元素都已排序完成,时间复杂度为n^2。（优化思路：当一次遍历前后数组不产生变化时，说明该数组已经有序，结束排序）

    代码：
        function bubbleSort(array){
            var len = array.length,i,j,temp,exchange,result;
            result = array.slice(0);
            for(i = 0; i < len; i++){
                exchange = 0;
                for(j = len - 1;j > i; j--){
                    if(result[j] < result[j-1]){
                        temp = result[j];
                        result[j] = result[j-1];
                        result[j-1] = temp;
                        exchange = 1;
                    }
                }
            if (!exchange) return result;
            }
            return result;
        }
        bubbleSort([44,1,3,6,2,55]); //[1, 2, 3, 6, 44, 55]

2、快速排序

    思想：首先选择一个元素（一般为中间元素）作为基准，然后比这个元素大的全部放在右边，比它小的全部放在左边；然后，在左边和右边分别重复上诉操作（时间复杂度为nlogn）。

    代码：
        function quickSort(array){
            sort = function(array){
                var len = array.length;
                if(len <= 1) return array;
                var pivotIndex = Math.floor(array.length / 2);
                var pivot = array.splice(pivotIndex, 1)[0];
                var left = [], right = [];
                for(var i = 0; i < len; i++){
                    if(array[i] < pivot){
                        left.push(array[i]);
                    }else{
                        right.push(array[i]);
                    }
                }
                return sort(left).concat([pivot], sort(right));
            }
            var result = sort(array);
            return result;
        }
    
