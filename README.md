# BinaryFind
a random int array, sort first, then use BinaryFind method to find any single element.




public class BinaryFind {

	public static void main(String[] args) {
		int[] arr0= {1,0,56,78,36,3,-4,8};//随意设定一个整数数组
		Selectsort sl0= new Selectsort(); 
		sl0.select(arr0); 
		for(int x:arr0) { //将排序后的数组打印出来.
			System.out.print(" "+x);
		}
		System.out.println();
		Bf bf0= new Bf();
		bf0.find(0, arr0.length-1, 36, arr0);
	}
}
//先用选择排序法给数组排序.
class Selectsort{
	public void select(int[] arr) {
		for(int i=0;i<arr.length;i++) {
			int min=arr[i];// 假设arr[i]是当前组中最小值,然后将其和后面arr[j]进行比较
			int minIndex=i;
			for(int j=i+1;j<arr.length;j++) {
				if(min>arr[j]) {
					min=arr[j];//如果有arr[j]比arr[i]小,则将更小的arr[j]值赋给min;
					minIndex=j;
				}
			}
			// j循环结束,找到了最小的值min,将其赋值给当前数组中最左边的元素arr[i](下一次i循环,就有更大的i,再赋值数组中第二小的值);
			int temp= arr[i]; // 用一个临时变量 temp来储存 arr[i];
			arr[i]= arr[minIndex];// 把找到的最小值赋值给 arr[i];
			arr[minIndex]= temp;// 交换arr[i]和arr[minIndex](即这一轮j循环里最小值arr[j])的值;
		}
	}	
}

//二分法查找.把数组分成左小右大两部分,查找,再细分,再查找.
class Bf{
	public void find(int leftindex,int rightindex,int value,int[] arr) {
		int mid=(leftindex+rightindex)/2;
		int midVal=arr[mid];
		if(leftindex<=rightindex)  { //设定左边下标要大于右边下标,以免find函数进入了死循环中.
			if(midVal<value) {			
				//此时说明要查找的value在中间值midVal的右边,我们下一步就去右边找.
				find(mid+1,rightindex,value,arr);				
			}else if(midVal>value) {
				//此时说明要查找的value在中间值midVal的左边,我们下一步就去左边找.
				find(leftindex,mid-1,value,arr);				
			}else if(midVal==value) {			
				//说明中间这个值就是我们要找的值.
				System.out.println("this is what we wanna find-- arr0["+mid+"] "+arr[mid]);
			}
		}else {
			System.out.println("we cant find it");
		}
	}
}
