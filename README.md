# Reflection Tutorial Modul 11

**Zufar Romli Amri**  
**NPM**: 2306202694  
**Kelas**: A

---

### Reflection on Hello Minikube

![/hello-minikube](./images/image-1.jpg)

![/hello-minikube](./images/image-2.jpg)

![/hello-minikube](./images/image-3.jpg)

![/hello-minikube](./images/image-4.jpg)

![/hello-minikube](./images/image-5.jpg)


## 1. Compare the application logs before and after you exposed it as a Service.Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?

Sebelum aplikasi di-expose sebagai Service, log aplikasi hanya menunjukkan bahwa HTTP server telah dimulai pada port 8080 dan UDP server pada port 8081. Pada tahap ini, aplikasi berjalan di dalam Pod tetapi tidak dapat diakses dari luar cluster. Setelah aplikasi di-expose menggunakan kubectl expose dan diakses melalui minikube service hellonode, log aplikasi akan menampilkan aktivitas tambahan setiap kali aplikasi dibuka melalui browser. Setiap permintaan HTTP yang masuk ke aplikasi akan tercatat dalam log, sehingga jumlah entri log akan bertambah setiap kali saya membuka atau me-refresh aplikasi di browser. Hal ini menunjukkan bahwa Service berhasil meneruskan traffic dari luar cluster ke Pod yang menjalankan aplikasi, dan setiap interaksi pengguna dengan aplikasi akan terekam dalam log container.

---

### 2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`.What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

Option -n dalam perintah kubectl get digunakan untuk menentukan namespace tertentu yang ingin dilihat resource-nya. Kubernetes menggunakan konsep namespace untuk memisahkan dan mengorganisir resource dalam sebuah cluster. Ketika menjalankan kubectl get pods atau kubectl get deployments tanpa option -n, kubectl akan menampilkan resource dari namespace "default" yang merupakan namespace bawaan untuk resource yang dibuat pengguna. Sedangkan ketika menggunakan kubectl get pods,services -n kube-system, perintah ini akan menampilkan resource dari namespace "kube-system" yang berisi komponen sistem Kubernetes seperti coredns, etcd, kube-apiserver, dan lain-lain. Namespace "kube-system" khusus digunakan untuk resource yang dikelola oleh sistem Kubernetes itu sendiri, bukan untuk aplikasi pengguna. Oleh karena itu, Pod dan Service yang saya buat secara eksplisit (seperti hellonode) tidak muncul dalam output kubectl get dengan option -n kube-system karena resource tersebut berada di namespace "default", bukan di namespace "kube-system".