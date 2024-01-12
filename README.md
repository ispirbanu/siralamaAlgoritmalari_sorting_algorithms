# Sıralama Algoritmaları

- **Selection sort -seçerek sıralama**
    
    sırasız diziyi sıralamak için dizideki tüm elemanları ilk olarak gezerek ardından bulduğu en küçük elemanı dizinin 1. elemanıyla yer değiştirir. ardından 2. elemandan itibaren tekrar bakarak tüm dizi sıralanana kadar devam eder.
    
    en iyi durumda da, ortalama ve en kötü durumda da n^2 olarak çalışır.
    
     
    
    ```python
    def selection_sort(arr):
        n = len(arr)
        for i in range(n - 1):
            min_index = i
            for j in range(i + 1, n):
                if arr[j] < arr[min_index]:
                    min_index = j
            # Min değeri bulduğumuz indeksle swap işlemi
            arr[i], arr[min_index] = arr[min_index], arr[i]
    
        return arr
    
    # Örnek kullanım:
    my_array = [64, 25, 12, 22, 11]
    sorted_array = selection_sort(my_array)
    print("Sıralanmış Dizi:", sorted_array)
    ```
    
    ### Selection C codu
    
    ```c
    #include <stdio.h>
    
    void selectionSort(int arr[], int n) {
        int i, j, minIndex, temp;
    
        for (i = 0; i < n - 1; i++) { //dizinin her elemanını gezerek minimum elemanın indisini bulma
            minIndex = i;
            for (j = i + 1; j < n; j++) { //i. elemandan sonraki elemanları kontrol ederek minimum elemanın indisini tespit eder.
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
    
            // Minimum elemanı bulunan indis ile değiştirme
            temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }
    }
    
    void printArray(int arr[], int size) {
        for (int i = 0; i < size; i++) {
            printf("%d ", arr[i]);
        }
        printf("\n");
    }
    
    int main() {
        int arr[] = {64, 25, 12, 22, 11};
        int n = sizeof(arr) / sizeof(arr[0]);
    
        printf("Sıralanmamış Dizi: \n");
        printArray(arr, n);
    
        selectionSort(arr, n);
    
        printf("\nSıralanmış Dizi: \n");
        printArray(arr, n);
    
        return 0;
    }
    //program çıktısı
    //Sıralanmamış Dizi:
    //64 25 12 22 11
    
    //Sıralanmış Dizi:
    //11 12 22 25 64
    ```
    

- ****Insertion Sort -Ekleme Sıralaması****
    
    baştan başlayarak elemanları gezer. geçtiği her elemanı bir öncekiyle kıyaslayarak küçükse yer değiştirir değilse sıralı olarak kabul ederek devam eder. 
    
    örneğin üçüncü eleman ilk iki elemandan küçükse önce kendinden bir öncekiyle karşılaştırır ve yer değiştirir ardından daha önceki yani ilk elemanla karşılaştırarak yer değiştirir. ardından kaldığı 4. indisteki değerle devam eder ve işlemler tekrarlanır.
    
    en kötü, ortalama durumda → n^2,   en iyi durumda → n , çünkü dizi sıralıysa üzerinde bir kere gezer.
    
    ```python
    def insertion_sort(arr):
        n = len(arr)
        for i in range(1, n):
            key = arr[i]
            j = i - 1
            while j >= 0 and key < arr[j]:
                arr[j + 1] = arr[j]
                j -= 1
            arr[j + 1] = key
    
        return arr
    
    # Örnek kullanım:
    my_array = [64, 25, 12, 22, 11]
    sorted_array = insertion_sort(my_array)
    print("Sıralanmış Dizi:", sorted_array)
    ```
    
    ### insertion sort C codu
    
    ```c
    #include <stdio.h>
    
    void insertionSort(int arr[], int n) {
        int i, key, j;
    
        for (i = 1; i < n; i++) { //dizinin her elemanını gezerek bir anahtar (key) belirler.
            key = arr[i];
            j = i - 1;
    
            // key'i, ondan önceki sıralı alt dizide doğru konumuna yerleştirme
    				//Anahtar, sıralı alt dizi içindeki elemanlardan daha küçük olduğu sürece ve
    				// j >= 0 olduğu sürece kaydırma işlemi yapılır.
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }
    
    void printArray(int arr[], int size) {
        for (int i = 0; i < size; i++) {
            printf("%d ", arr[i]);
        }
        printf("\n");
    }
    
    int main() {
        int arr[] = {64, 25, 12, 22, 11};
        int n = sizeof(arr) / sizeof(arr[0]);
    
        printf("Sıralanmamış Dizi: \n");
        printArray(arr, n);
    
        insertionSort(arr, n);
    
        printf("\nSıralanmış Dizi: \n");
        printArray(arr, n);
    
        return 0;
    }
    //Sıralanmamış Dizi: 
    // 64 25 12 22 11
    
    //Sıralanmış Dizi: 
    // 11 12 22 25 64
    ```
    

- ****Bubble Sort -Kabarcık / Baloncuk Sıralması****
    
    diziyi sıralamak için her seferinde iki elemana bakarak tüm dizi içerisinde gezinir.
    
    ör. 5,7,2,9,6,1,3 elemanlarından oluşan bir dizi olsun. her seferinde ikili olarak hareket edip bu elemanları yer değiştirerek n-1 kadar hareket ettikten sonra bu işleme devam edecek.
    
![Untitled](https://github.com/ispirbanu/siralamaAlgoritmalari_sorting_algorithms/assets/45195137/3d23efe0-24f0-4af0-a7a3-07803429ecae)

    
    şeklinde ilerleyerek dizi sıralı hale gelene kadar devam eder.
    
    en kötü , ortalama  durum → n^2,    en iyi durum→n  bu da sıralı olduğu durumdur. (bunu da bir kere geçtikten sonra eleman değişmeme kontrolü yapmak gerekiyor.)
    
    ```python
    def bubble_sort(arr):
        n = len(arr)
        for i in range(n - 1):
            # Her turda en büyük eleman zaten doğru konuma yerleşeceği için son i elemanı dikkate almıyoruz
            for j in range(0, n - i - 1):
                # Komşu elemanları karşılaştır ve sırala
                if arr[j] > arr[j + 1]:
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
    
        return arr
    
    # Örnek kullanım:
    my_array = [64, 25, 12, 22, 11]
    sorted_array = bubble_sort(my_array)
    print("Sıralanmış Dizi:", sorted_array)
    ```
    
    ### bubble sort C codu
    
    ```c
    #include <stdio.h>
    
    void bubbleSort(int arr[], int n) {
        int i, j, temp;
        for (i = 0; i < n-1; i++) { //i değişkeni, dizideki elemanları tek tek kontrol etmek için kullanılır. Bu döngü, dizinin tamamını bir kez geçene kadar devam eder.
            for (j = 0; j < n-i-1; j++) { //j değişkeni, her geçişte dizinin kalan kısmını kontrol etmek için kullanılır. 
    //Bu döngü, n - i - 1 kez çalışır çünkü her geçişte en büyük eleman zaten doğru konumuna yerleşmiş olur.
                if (arr[j] > arr[j+1]) {
                    // Elemanların yerini değiştirme
    // Eğer arr[j] daha büyükse, elemanlar yer değiştirir. Bu, küçükten büyüğe sıralama amacını taşır.
                    temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
    }
    
    void printArray(int arr[], int size) {
        for (int i = 0; i < size; i++) {
            printf("%d ", arr[i]);
        }
        printf("\n");
    }
    
    int main() {
        int arr[] = {64, 25, 12, 22, 11};
        int n = sizeof(arr) / sizeof(arr[0]);
    
        printf("Sıralanmamış Dizi: \n");
        printArray(arr, n);
    
        bubbleSort(arr, n);
    
        printf("\nSıralanmış Dizi: \n");
        printArray(arr, n);
    
        return 0;
    }
    ```
    

- **Merge Sort- Birleştirme sıralaması**
    
    problem parçalara bölünür
    
    bölünen parçalar çözülür
    
    çözülen parçalar birleştirilir.
    
    1. **Bölme (Divide):** Verilen diziyi ortadan iki parçaya böler.
    2. **İkili Böl (Conquer):** Her iki parçayı ayrı ayrı sıralar. Bu adım, parçaların boyutu 1 veya 0 olana kadar devam eder.
    3. **Birleştirme (Merge):** İki sıralı parçayı birleştirerek tek bir sıralı dizi oluşturur.
    
    ```python
    def merge_sort(arr):
        if len(arr) > 1:
            mid = len(arr) // 2  # Diziyi ortadan ikiye böler
    
            left_half = arr[:mid]  # Sol yarıyı alır
            right_half = arr[mid:]  # Sağ yarıyı alır
    
            merge_sort(left_half)  # Sol yarıyı sıralar
            merge_sort(right_half)  # Sağ yarıyı sıralar
    
            i = j = k = 0
    
            # İki parçayı birleştirme
            while i < len(left_half) and j < len(right_half):
                if left_half[i] < right_half[j]:
                    arr[k] = left_half[i]
                    i += 1
                else:
                    arr[k] = right_half[j]
                    j += 1
                k += 1
    
            # Eğer sol tarafta elemanlar kalmışsa
            while i < len(left_half):
                arr[k] = left_half[i]
                i += 1
                k += 1
    
            # Eğer sağ tarafta elemanlar kalmışsa
            while j < len(right_half):
                arr[k] = right_half[j]
                j += 1
                k += 1
    
    # Örnek kullanım
    arr = [64, 25, 12, 22, 11]
    print("Sıralanmamış Dizi:", arr)
    
    merge_sort(arr)
    
    print("Sıralanmış Dizi:", arr)
    ```
    
    ### Merge sort C Codu
    
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    
    void merge(int arr[], int left, int mid, int right) {
        int i, j, k;
        int n1 = mid - left + 1;
        int n2 = right - mid;
    
        // Geçici diziler oluşturulur
        int LeftArr[n1], RightArr[n2];
    
        // Geçici dizilere veriler kopyalanır
        for (i = 0; i < n1; i++)
            LeftArr[i] = arr[left + i];
        for (j = 0; j < n2; j++)
            RightArr[j] = arr[mid + 1 + j];
    
        // Geçici diziler birleştirilir
        i = 0;
        j = 0;
        k = left;
        while (i < n1 && j < n2) {
            if (LeftArr[i] <= RightArr[j]) {
                arr[k] = LeftArr[i];
                i++;
            } else {
                arr[k] = RightArr[j];
                j++;
            }
            k++;
        }
    
        // Geriye kalan elemanlar eklenir
        while (i < n1) {
            arr[k] = LeftArr[i];
            i++;
            k++;
        }
    
        while (j < n2) {
            arr[k] = RightArr[j];
            j++;
            k++;
        }
    }
    
    void mergeSort(int arr[], int left, int right) {
        if (left < right) {
            // Diziyi ortadan ikiye böler
            int mid = left + (right - left) / 2;
    
            // Her iki yarıyı sıralar
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
    
            // Sıralı yarıları birleştirir
            merge(arr, left, mid, right);
        }
    }
    
    void printArray(int A[], int size) {
        for (int i = 0; i < size; i++)
            printf("%d ", A[i]);
        printf("\n");
    }
    
    int main() {
        int arr[] = {64, 25, 12, 22, 11};
        int arr_size = sizeof(arr) / sizeof(arr[0]);
    
        printf("Sıralanmamış Dizi: \n");
        printArray(arr, arr_size);
    
        // Merge Sort'u uygula
        mergeSort(arr, 0, arr_size - 1);
    
        printf("\nSıralanmış Dizi: \n");
        printArray(arr, arr_size);
    
        return 0;
    }
    ```
    
- 
- ************Yığın (Heap) ve Yığın Sıralaması (Heap Sort)************
