<p align="center" >
  <b>POINT UTAMA</b>
</p>

---

> #### INSTALASI
> - PHP 8.1.0
> - LARAVEL 10.2.5
>   ```
>   Composer Create-project laravel\laravel=v10.2.4 laravel-eloquent-api-resource
>   ```
---
> #### CARA MENJALANKAN PROGRAM
> ```
> php artisan serve
> ```
---
> #### ELOQUENT API RESOURCE
> - Eloquent API Resource adalah alat dalam Laravel untuk mengatur dan menampilkan data dari model dalam format yang sesuai untuk respons API. Ini memungkinkan Anda mengontrol dengan tepat bagaimana data disajikan dalam respons API, termasuk properti yang disertakan, disembunyikan, dan format data yang diinginkan.
> 
> #### MODEL
> - model dalam Laravel adalah representasi kelas dari entitas basis data, sedangkan Eloquent API Resource adalah alat untuk mengatur dan menampilkan data dari model dalam format yang sesuai untuk respons API.
> 
> #### RESOURCE
> - Resource dalam Laravel adalah kelas yang mengelola dan memformat data untuk respons API. Mereka memungkinkan Anda menyesuaikan bagaimana data disajikan, mengubah format, dan melakukan transformasi sebelum dikirimkan ke klien. Ini membantu menjaga kode Anda terorganisir dan memberikan kontrol atas representasi data dalam API Anda.
>   
> #### RESOURCE COLLECTION
> - Resource collection dalam Laravel adalah kelas yang membantu Anda mengelola kumpulan data yang akan dikirim sebagai respons API. Mereka memungkinkan penyesuaian format dan transformasi data sebelum dikirimkan ke klien, menjaga kode Anda tetap terstruktur dan bersih.
> 
> #### NESTED RESOURCE
> - Nested Resource dalam Laravel adalah cara untuk mengelola hubungan bersarang (nested) antara model dalam respons API. Ini terutama berguna ketika Anda memiliki hubungan one-to-many atau many-to-many antara model, di mana satu model terkait dengan satu atau lebih instance dari model lainnya.
> 
> #### DATA WRAP
> - Data wrapping adalah proses menyertakan data tambahan di dalam respons API. Ini dapat berguna untuk menyediakan informasi tambahan kepada pengguna, seperti metadata, pesan status, atau data lain yang relevan dengan respons yang dikirimkan.
> - Dalam konteks Laravel, Anda bisa menggunakan konsep data wrapping dengan resource. Misalnya, Anda bisa membuat wrapper untuk respons API Anda dengan menambahkan data tambahan di samping data utama yang dikirimkan.
>
> 
> Berikut adalah contoh kode menggunakan data wrapping:
>  ```
>
>public function show($id)
>{
>    $post = Post::find($id);
>    
>    return response()->json([
>        'data' => new PostResource($post),
>        'status' => 'success',
>        'message' => 'Data post berhasil.'
>    ]);
>}
>```
> 
> #### DATA WRAP COLLECTION
> - Data wrap collection adalah proses menyertakan data tambahan di dalam koleksi data yang dikirim sebagai respons API. Ini berguna untuk memberikan informasi tambahan kepada pengguna, seperti metadata, pesan
status, atau data lain yang relevan dengan koleksi yang dikirimkan.
> - Dalam konteks Laravel, Anda dapat menggunakan konsep data wrap collection dengan menggunakan resource collection. Resource collection memungkinkan Anda untuk menyesuaikan format respons untuk koleksi data.
> - Berikut adalah contoh sederhana menggunakan data wrap collection dalam respons API dengan Laravel:
> ```
> use App\Http\Resources\PostResource;
>
>public function index()
>{
>    $posts = Post::all();
>    
>    // Data wrap collection dengan resource collection
>    return response()->json([
>        'data' => PostResource::collection($posts),
>        'status' => 'success',
>        'message' => 'Data posts berhasil diambil.'
>    ]);
>}
>```
> 
> #### PAGINATION
> - Pagination adalah proses membagi hasil query menjadi sejumlah halaman yang dapat ditampilkan, sehingga memungkinkan pengguna untuk menavigasi melalui data dengan lebih mudah. Ini sangat penting ketika Anda memiliki kumpulan data yang besar, karena memungkinkan pengguna untuk mengakses data secara bertahap, mengurangi waktu loading dan memperbaiki kinerja aplikasi secara keseluruhan.
> 
> Berikut contoh kode pagination :
> ```
>public function index()
>{
>    $posts = Post::paginate(10); // Menentukan jumlah item per halaman (10)
>
>    return PostResource::collection($posts);
>}
>```
> #### CONDITIONAL ATTRIBUTES
> - Conditional attributes dalam Laravel Resource adalah cara untuk menyertakan atribut dalam respons API berdasarkan kondisi tertentu. Ini berguna ketika Anda ingin menyertakan atribut hanya jika kondisi tertentu terpenuhi.
>
> 
> Berikut adalah contoh kode conditional attributes:
> ```
>
>class PostResource extends JsonResource
>{
>    public function toArray($request)
>    {
>        return [
>            'id' => $this->id,
>            'title' => $this->title,
>            'content' => $this->when($this->is_published, $this->content),
>            'created_at' => $this->created_at,
>            'updated_at' => $this->updated_at,
>        ];
>    }
>}
>```
> #### RESOURCE RESPONSE
> - Resource response dalam konteks Laravel adalah respons yang dihasilkan oleh menggunakan resource untuk memformat data sebelum dikirimkan sebagai respons dari endpoint API. Resource digunakan untuk mengubah representasi model menjadi format yang diinginkan sebelum dikirimkan ke klien.
> 
> - Berikut contoh kode resource response:
> ```
>
>public function show($id)
>{
>    $post = Post::findOrFail($id);
>
>    return new PostResource($post);
>}
>```

<p align="center" >
  <b>KESIMPULAN</b>
</p>


















