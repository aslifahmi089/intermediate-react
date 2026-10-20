# React Lifecycle Methods & Hooks

## Implementasi

### A. Menggunakan useEffect

`useEffect` adalah React Hook yang digunakan untuk menyinkronkan komponen dengan sistem eksternal, misalnya timer, event listener, atau koneksi jaringan.

**Contoh kode:**

```jsx
import { useEffect, useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Jumlah klik: ${count}`;
  }, [count]);

  return (
    <div>
      <h2>Jumlah klik: {count}</h2>
      <button onClick={() => setCount(count + 1)}>
        Tambah
      </button>
    </div>
  );
}
```

**Penjelasan:**

- `useState(0)` menyimpan nilai counter.
- `useEffect()` menjalankan efek setelah React melakukan pembaruan tampilan.
- `[count]` merupakan array dependensi yang membuat effect dijalankan kembali ketika nilai `count` berubah.
- `document.title` mengubah judul tab browser sesuai jumlah klik.

### B. Memahami Array Dependensi

Array dependensi menentukan kapan suatu effect perlu dijalankan kembali.

**Contoh kode:**

```jsx
import { useEffect } from 'react';

useEffect(() => {
  console.log('Effect dijalankan setelah render');
});

useEffect(() => {
  console.log('Effect dengan dependensi kosong');
}, []);

useEffect(() => {
  console.log('Nilai nama berubah');
}, [name]);
```

**Penjelasan:**

- Tanpa array dependensi, effect dijalankan setelah setiap render yang selesai.
- Dengan `[]`, effect dijalankan saat komponen dipasang, dengan catatan React Strict Mode dapat menjalankan siklus tambahan dalam lingkungan pengembangan.
- Dengan `[name]`, effect dijalankan saat komponen dipasang dan ketika nilai `name` berubah.

### C. Menggunakan Fungsi Cleanup

Fungsi cleanup digunakan untuk membersihkan efek samping, misalnya menghentikan timer atau melepaskan event listener.

**Contoh kode:**

```jsx
import { useEffect, useState } from 'react';

export default function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setSeconds((previous) => previous + 1);
    }, 1000);

    return () => {
      clearInterval(timer);
    };
  }, []);

  return <h2>Waktu berjalan: {seconds} detik</h2>;
}
```

**Penjelasan:**

- `setInterval()` menjalankan fungsi setiap satu detik.
- `setSeconds()` memperbarui nilai waktu.
- Fungsi cleanup memanggil `clearInterval(timer)` untuk menghentikan timer ketika effect dibersihkan.
- Cleanup juga dijalankan sebelum effect diulang karena dependensinya berubah, jika terdapat dependensi yang berubah.


## Kesimpulan

Lifecycle menggambarkan tahapan keberadaan komponen React, sedangkan effect memiliki siklus sinkronisasi berupa menjalankan setup dan membersihkan efek ketika diperlukan. `useEffect` membantu menyinkronkan komponen dengan sistem eksternal, array dependensi menentukan kapan effect perlu dijalankan kembali, dan fungsi cleanup digunakan untuk menghentikan atau membersihkan proses yang sudah tidak diperlukan.
