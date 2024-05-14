<p align="center" >
  <b>POINT UTAMA</b>
</p>

---

> #### INSTALASI
> - PHP 8.1.0
> - LARAVEL 10.2.4
>   ```
>   Composer Create-project laravel\laravel=v10.2.4 laravel-eloquent
>   ```
> - XAMPP
---
> #### CARA MENJALANKAN PROGRAM
> ```
> php artisan serve
> ```
---
> #### APA ITU LARAVEL ELOQUENT?
> - Eloquent dalam Laravel adalah ORM (Object-Relational Mapping) yang memungkinkan Anda berinteraksi dengan database menggunakan objek-objek PHP.
>
> #### INSERT
> - Dalam konteks Laravel Eloquent, "insert" merujuk pada operasi untuk menyimpan data baru ke dalam database. Anda dapat menggunakan metode create() pada model Eloquent untuk melakukan operasi insert.
>
> Berikut contoh insert pada laravel eloquent :
> ```
> $user = User::create([
>    'name' => 'Farel',
>    'email' => 'farel@localhost',
> ]);
> ```
>
> #### FIND
> - Dalam Laravel Eloquent, "find" adalah metode yang digunakan untuk menemukan satu record dalam tabel database berdasarkan nilai kunci primernya (biasanya bernama "id"). 
>
> Berikut contoh kode raw sql :
> ```
> 
> ```
>
> #### DATABASE TRANSACTION
> - Laravel database juga memiliki fitur untuk melakukan database transaction secara otomatis
> - kita bisa menggunakan function ```DB::transaction```
>
> Berikut salah satu contoh kode database transaction :
> ```
> // Manual database transaction
> DB::transaction(function () {
> DB::insert('insert into categories(id, name, description, created_at) values (?, ?, ? , ?)', [
> "GADGET", "Gadget", "Gadget Category", "2020-10-10 10:10:10"
> ]);
> DB::insert('insert into categories(id, name, description, created_at) values (?, ?, ? , ?)', [
> "FOOD", "Food", "Food Category", "2020-10-10 10:10:10"
> ]);
> });
> ```
> #### QUERY BUILDER INSERT
> - Untuk melakukan insert menggunakan query builder, kita bisa menggunakan method dengan prefix insert dengan parameter associative array dimana key nya adalah kolom, dan valuenya nilai yang akan disimpan diatabase
> - InsertGetId() untuk memasukan data ke database, dan mengembalikan primary key yang diset secara auto generetae, cocok untuk tabel dengan id auto increment
> - insertOrIgnore() untuk memasukan data ke database dan jika terjadi error maka akan di ignore
>
> Berikut contoh kode query builder insert :
> ```
> DB::table("categories")->insert([
>     "id" => "GADGET",
>     "name" => "Gadget"
> ]);
>  DB::table("categories")->insert([
>     "id" => "FOOD",
>     "name" => "Food"
>
> ]);
>
> $result = DB::select("select count(id) as total from categories");
> self::assertEquals(2, $result[0]->total);
> ```
---
> #### QUERY BUILDER SELECT
> - Query builder select bisa kita gunakan untuk mengubah select kolom dimana defaultnya adalah semua kolom
>
> Berikut salah satu contoh kode query builder select :
> ```
> $this->testInsert();
>
> $collection = DB::table("categories")->select(["id", "name"])->get();
> self::assertNotNull($collection);
>
> $collection->each(function ($item) {
>     Log::info(json_encode($item));
> });
> ```
> #### CHUNK RESULT
> - Chunk Result dalam Laravel Query Builder memungkinkan Anda untuk membagi hasil query menjadi beberapa bagian (chunk) yang lebih kecil untuk diproses secara terpisah. Ini berguna ketika Anda perlu memproses jumlah data besar tanpa membebani memori server secara berlebihan.
>
> Berikut contoh kode chunk result :
> ```
> $this->insertManyCategories();
>
> DB::table("categories")->orderBy("id")
>     ->chunk(10, function ($categories) {
>         self::assertNotNull($categories);
>         Log::info("Start Chunk");
>         $categories->each(function ($category) {
>     Log::info(json_encode($category));
> });
> Log::info("End Chunk");
> });
> ```
>
> #### LAZY RESULT
> - Laravel memiliki fitur lazy, dimana kita bisa menjadikan query builder dengan lazy results, yang menghasilkan lazy collection
> - karena hasilnya berupa lazy, data yang diambil dari database akan bertahap tidak langsung semuanya diload ke memory
>
> Berikut contoh salah satu kode lazy results :
> ```
> $this->insertManyCategories();
>
> $collection = DB::table("categories")->orderBy("id")->lazy(10)->take(3);
> self::assertNotNull($collection);
>
> $collection->each(function ($item) {
>     Log::info(json_encode($item));
> });
> ```
>
> #### CURSOR
> - Selain chunk dan lazy, terdapat cara lain untuk membuat lazy result, yaitu menggunakan cursor
> - cursor hanya akan melakukan query satu kali
>
> Berikut contoh kode cursor :
> ```
> $this->insertManyCategories();
> 
> $collection = DB::table("categories")->orderBy("id")->cursor();
> self::assertNotNull($collection);
>
> $collection->each(function ($item) {
>     Log::info(json_encode($item));
> });
> ```
>
> #### PAGINATION
> - Daat kita membuat aplikasi Web atau RESTful API yang mengembalikan data di database, kita sering memberi informasi tentang pagination, misal jumlah record, jumlah page, page saat ini dan lain lain
> - Pagination dalam Laravel memungkinkan Anda untuk membagi hasil query menjadi beberapa halaman untuk ditampilkan kepada pengguna secara terpisah.
>
> Berikut contoh kode pagination :
> ```
> $this->insertCategories();
>
> $paginate = DB::table("categories")->paginate(perPage: 2, page: 2);
>
> self::assertEquals(2, $paginate->currentPage());
> self::assertEquals(2, $paginate->perPage());
> self::assertEquals(2, $paginate->lastPage());
> self::assertEquals(4, $paginate->total());
>
> $collection = $paginate->items();
> self::assertCount(2, $collection);
> foreach ($collection as $item) {
>     Log::info(json_encode($item));
> }
> ```
>
> #### GROUPING
> - Grouping dalam Laravel Collection adalah proses mengelompokkan elemen-elemen koleksi berdasarkan kriteria tertentu, seperti properti atau hasil dari sebuah closure.
>
> Berikut contoh kode grouping :
> ```
> $collection = collect([
>     [
>         "name" => "Farel",
>         "department" => "IT"
>     ],
>     [
>         "name" => "Zeta",
>         "department" => "IT"
>     ],
>     [
>         "name" => "Takku",
>         "department" => "HR"
>     ]
> ]);
>
> $result = $collection->groupBy("department");
> ```
>
> #### DATABASE MIGRATION
> - Laravel memiliki fitur bernama database migration, fitur ini digunakan untuk melakukan versioning schema database, dimana setiap perubahan akan di track sehingga akan selalu konsisten
>
> Berikut contoh kode membuat database migration :
> ```
> // pada terminal
> php artisan make:migration create_table_counter
>
> // untuk migrate database ke dalam database mysql
> php artisan migrate
> ```
> 
> #### DATABASE SEEDING
> - Database Seeding dalam Laravel adalah proses untuk memasukkan data awal ke dalam tabel database Anda. Ini berguna saat Anda ingin mengisi database dengan data contoh atau data yang dibutuhkan untuk pengujian atau pengembangan.
>
> Berikut contoh kode database seeding :
> ```
> // membuat seed baru
> php artisan make:seed CategorySeeder
>
> // Contoh kode seeder
> public function run(): void
> {
> DB::table("counters")->insert([
> "id" => "sample",
> "counter" => 0
> ]);
> }
>
> // Untuk mengseed database lakukan
> php artisan db:seed
> ```
<p align="center" >
  <b>PERTANYAAN DAN CATATAN TAMBAHAN</b>
</p>

---

> - 

---

<p align="center" >
  <b>KESIMPULAN</b>
</p>


















