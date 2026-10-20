# React Conditional Rendering & Lists
## Implementasi

### A. Conditional Rendering

Conditional rendering adalah teknik untuk menampilkan elemen berdasarkan kondisi tertentu. React dapat menggunakan kondisi JavaScript untuk menentukan tampilan yang sesuai.

**Contoh kode:**

```jsx
function UserStatus({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h2>Selamat datang kembali!</h2>;
  }

  return <h2>Silakan login terlebih dahulu.</h2>;
}

export default function App() {
  return (
    <div>
      <UserStatus isLoggedIn={true} />
      <UserStatus isLoggedIn={false} />
    </div>
  );
}
```

**Penjelasan:**

- `UserStatus` menerima props `isLoggedIn`.
- Jika nilainya `true`, komponen menampilkan pesan selamat datang.
- Jika nilainya `false`, komponen menampilkan pesan untuk login.
- React menampilkan hasil sesuai kondisi yang diberikan.

**Output yang diharapkan:**

```text
Selamat datang kembali!
Silakan login terlebih dahulu.
```

### B. Rendering Lists Menggunakan map()

Method `map()` digunakan untuk mengolah setiap item dalam sebuah array dan menghasilkan elemen JSX untuk ditampilkan dalam React.

**Contoh kode:**

```jsx
const fruits = ['Apel', 'Jeruk', 'Mangga'];

export default function FruitList() {
  return (
    <ul>
      {fruits.map((fruit) => (
        <li key={fruit}>{fruit}</li>
      ))}
    </ul>
  );
}
```

**Penjelasan:**

- `fruits` merupakan array yang berisi daftar buah.
- `map()` mengolah setiap item dalam array.
- Setiap item ditampilkan sebagai elemen `<li>`.
- `key={fruit}` memberikan identitas unik untuk setiap item dalam daftar tersebut.

**Output yang diharapkan:**

- Apel
- Jeruk
- Mangga

### C. Menggunakan Conditional Rendering dan Lists

Kedua konsep dapat digunakan bersama untuk menampilkan daftar data berdasarkan kondisi tertentu.

**Contoh kode:**

```jsx
const tasks = [
  { id: 1, name: 'Belajar JSX', completed: true },
  { id: 2, name: 'Belajar Props', completed: true },
  { id: 3, name: 'Belajar Rendering', completed: false },
];

export default function TaskList() {
  const completedTasks = tasks.filter(
    (task) => task.completed
  );

  return (
    <div>
      <h2>Daftar Tugas Selesai</h2>

      {completedTasks.length > 0 ? (
        <ul>
          {completedTasks.map((task) => (
            <li key={task.id}>{task.name}</li>
          ))}
        </ul>
      ) : (
        <p>Belum ada tugas yang selesai.</p>
      )}
    </div>
  );
}
```

**Penjelasan:**

- `filter()` memilih tugas yang memiliki nilai `completed` berupa `true`.
- Operator ternary memeriksa apakah terdapat tugas yang selesai.
- `map()` menampilkan setiap tugas yang memenuhi kondisi.
- `key={task.id}` digunakan untuk memberikan identitas unik pada setiap item.
- Jika tidak ada tugas yang selesai, React menampilkan pesan alternatif.

**Output yang diharapkan:**

```text
Daftar Tugas Selesai

Belajar JSX
Belajar Props
```

## 4. Proof of Understanding (Bukti Pemahaman)

Bukti pemahaman dilakukan melalui implementasi langsung conditional rendering dan lists dalam aplikasi React.

Implementasi yang dikerjakan meliputi:

1. Membuat komponen yang menampilkan tampilan berbeda berdasarkan kondisi menggunakan `if`.
2. Membuat daftar data menggunakan method `map()`.
3. Menambahkan `key` yang unik dan stabil pada setiap item daftar.
4. Menggabungkan `filter()`, `map()`, dan conditional rendering untuk menampilkan data sesuai kondisi.
5. Menguji kondisi ketika daftar berisi data dan ketika tidak ada data yang memenuhi kondisi.
6. Mendokumentasikan source code serta hasil pengujian di GitHub.

## 5. Kesimpulan

Conditional rendering memungkinkan React menampilkan elemen berdasarkan kondisi tertentu, sedangkan method `map()` memungkinkan data dalam array ditampilkan sebagai daftar elemen JSX. Penggunaan `key` membantu React mengidentifikasi setiap item dalam daftar. Ketiga konsep tersebut dapat dikombinasikan untuk membangun antarmuka yang dinamis sesuai kondisi dan data yang tersedia.

- [React — Conditional Rendering](https://react.dev/learn/conditional-rendering)
- [React — Rendering Lists](https://react.dev/learn/rendering-lists)
