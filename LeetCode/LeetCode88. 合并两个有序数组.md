# 88. 合并两个有序数组
## 题目
给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

说明:
- 初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
- 你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。


## eg1

输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]


## 默认代码模板

	class Solution {
	public:
	    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
	        
	    }
	};

## 正确解法
把nums2的元素都放入nums1，然后用sort函数进行排序

**注意，sort的用法 sort(nums1.begin(), nums1.end())**

---
	class Solution {
	public:
	    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
	        int j = 0;
	        for(int i = m; j < n; i++)
	        {
	            nums1[i] = nums2[j];
	            j++;
	        }
	        sort(nums1.begin(), nums1.end());
	    }
	};
---