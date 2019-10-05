# Data Structure

## Sort
#### Insertiong Sort (삽입 정렬)
```java
public static void insertionSort(int list[]) {
	final int SIZE = list.length;
	for (int i = 1; i < SIZE; i++) { // U집합
		int temp = list[i];
		for (int j = 0; j < i; j++) { // S집합
			if (temp < list[j]) { // 삽입 위치
				for (int k = i - 1; k >= j; k--) {
					// S집합 끝부터 하나씩 삽입위치원소까지 뒤로 이동
					list[k + 1] = list[k];
				}
				list[j] = temp;
				break;
			}
		}
	}
}
```
#### Merge Sort (병합 정렬)
```java
public class MergeSortTest {
	public static void mergeSort(int[] list, int start, int end) {
		// 현집합을 반으로 나누어 정렬
		if (start == end) return;
		
		int half = (start + end) / 2;
		// 왼쪽집합 정렬해오기
		mergeSort(list, start, half);
		// 오른쪽집합 정렬해오기
		mergeSort(list, half+1, end);
		// 정렬된 두 집합 이용하여 합치기
		merge(list, start, half, end);
	}

	private static void merge(int[] list, int start, int half, int end) {
		int newArr[] = new int[end - start + 1];
		int left = start, right = half + 1;
		int i = 0;
		
		do {
			if (list[left] < list[right]) {
				newArr[i++] = list[left++];
			} else {
				newArr[i++] = list[right++];
			}
		} while (left <= half && right <= end);
		
		// 왼쪽 집합이 남은 경우 (오른쪽 집합은 다 처리됨)
		while (left <= half) newArr[i++] = list[left++];
		// 오른쪽 집합이 남은 경우 (왼쪽 집합은 다 처리됨)
		while (right <= half) newArr[i++] = list[right++];
		
		System.arraycopy(newArr, 0, list, start, newArr.length);
	}
	
	public static void main(String[] args) {
		int[] list = { 69, 10, 30, 2, 16, 8, 31, 22 };
		System.out.println(Arrays.toString(list));
		mergeSort(list, 0, list.length - 1);
		System.out.println(Arrays.toString(list));
	}
}
```

#### Quick Sort
```java
public class QuickSortTest {
	
	static int[] arr = { 69, 10, 30, 30, 2, 16, 8, 31, 22 };
	
	public static void main(String[] args) {
		quickSort(arr, 0, arr.length - 1);
		System.out.println(Arrays.toString(arr));
	}
	
	static void quickSort(int[] arr, int start, int end) {
		if (start < end) {						// 집합의 크기가 2이상일 경우만 정렬 시도
			int pivot = fixPivot(arr, start, end);
			quickSort(arr, 0, pivot - 1); // 왼쪽
			quickSort(arr, pivot + 1, end); // 오른쪽
		}
	}

	private static int fixPivot(int[] arr2, int start, int end) {
		int pivot = start;
		int left = start + 1;
		int right = end;
		do {
			while (left < end && arr[left] < arr[pivot]) left += 1;
			while (right > start && arr[right] >= arr[pivot]) right -= 1;
			
			if (left < right) {
				int tmp = arr[left];
				arr[left] = arr[right];
				arr[right] = tmp;
			}
		} while (left < right);
		
		int tmp = arr[pivot];
		arr[pivot] = arr[right];
		arr[right] = tmp;
		return right;
	}
	
}
```
