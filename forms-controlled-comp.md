# React Forms & Controlled Components
## Implementasi

### A. Membuat Controlled Component

Controlled component adalah elemen input yang nilai tampilannya dikendalikan oleh state React melalui properti `value`. Perubahan nilai input ditangani melalui event handler seperti `onChange`.

**Contoh kode:**

```jsx
import { useState } from 'react';

export default function NameForm() {
  const [name, setName] = useState('');

  return (
    <div>
      <label htmlFor="name">Nama:</label>

      <input
        id="name"
        type="text"
        value={name}
        onChange={(event) => setName(event.target.value)}
        placeholder="Masukkan nama"
      />

      <p>Nama: {name}</p>
    </div>
  );
}
```

**Penjelasan:**

- `useState('')` menyimpan nilai nama dengan nilai awal berupa string kosong.
- `value={name}` menghubungkan nilai input dengan state.
- `onChange` menangani perubahan nilai yang dimasukkan pengguna.
- `setName(event.target.value)` memperbarui state berdasarkan input terbaru.
- Teks nama di bawah input berubah sesuai nilai yang dimasukkan.

### B. Membuat Formulir dengan onSubmit

Pada implementasi berikutnya, formulir digunakan untuk menerima nama dan email, kemudian menampilkan hasil ketika pengguna menekan tombol kirim.

**Contoh kode:**

```jsx
import { useState } from 'react';

export default function RegistrationForm() {
  const [form, setForm] = useState({
    name: '',
    email: '',
  });

  const [message, setMessage] = useState('');

  function handleChange(event) {
    const { name, value } = event.target;

    setForm((previous) => ({
      ...previous,
      [name]: value,
    }));
  }

  function handleSubmit(event) {
    event.preventDefault();

    setMessage(
      `Pendaftaran berhasil untuk ${form.name} (${form.email}).`
    );
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="name">Nama:</label>
        <input
          id="name"
          name="name"
          type="text"
          value={form.name}
          onChange={handleChange}
          required
        />
      </div>

      <div>
        <label htmlFor="email">Email:</label>
        <input
          id="email"
          name="email"
          type="email"
          value={form.email}
          onChange={handleChange}
          required
        />
      </div>

      <button type="submit">Kirim</button>

      {message && <p>{message}</p>}
    </form>
  );
}
```

**Penjelasan:**

- State `form` menyimpan nilai nama dan email.
- `handleChange()` memperbarui field yang sesuai berdasarkan atribut `name` pada input.
- Operator spread `...previous` mempertahankan nilai field lainnya ketika salah satu input berubah.
- `onSubmit` menjalankan fungsi ketika formulir dikirim.
- `event.preventDefault()` mencegah formulir memuat ulang halaman secara default.
- `required` memastikan kedua input harus diisi sebelum formulir dapat dikirim melalui browser.
- State `message` menyimpan dan menampilkan pesan setelah formulir dikirim.

**Output yang diharapkan:**

Jika pengguna mengisi nama `Fahmi` dan email `fahmi@example.com`, lalu menekan tombol Kirim, aplikasi menampilkan:

```text
Pendaftaran berhasil untuk Fahmi (fahmi@example.com).
```

Pesan tersebut merupakan simulasi keberhasilan pada sisi antarmuka, bukan bukti bahwa data telah tersimpan ke database.

### C. Mengenal Formik

Formik merupakan library yang membantu mengelola formulir dalam React, terutama ketika formulir memiliki banyak field, validasi, dan proses pengiriman data.

Formik menyediakan beberapa fitur, seperti:

- Pengelolaan nilai input.
- Penanganan perubahan dan pengiriman formulir.
- Pengelolaan status validasi dan pesan kesalahan.
- Pengelolaan status pengiriman formulir.

Contoh penggunaan dasar Formik:

```jsx
import { Formik, Form, Field } from 'formik';

export default function FormikExample() {
  return (
    <Formik
      initialValues={{ name: '' }}
      onSubmit={(values) => {
        alert(`Halo, ${values.name}!`);
      }}
    >
      <Form>
        <label htmlFor="name">Nama:</label>

        <Field
          id="name"
          name="name"
          placeholder="Masukkan nama"
        />

        <button type="submit">Kirim</button>
      </Form>
    </Formik>
  );
}
```

**Penjelasan:**

- `Formik` mengelola state dan proses formulir.
- `initialValues` menentukan nilai awal field.
- `Field` menyediakan input yang terhubung dengan pengelolaan formulir Formik.
- `Form` menangani struktur dan pengiriman formulir.
- `onSubmit` menerima nilai formulir ketika pengguna mengirimkannya.

Untuk menjalankan contoh ini, instal Formik terlebih dahulu menggunakan perintah `npm install formik`.


## Kesimpulan

Forms & Controlled Components merupakan konsep penting dalam pengelolaan input pengguna di React. Dengan `useState`, nilai input dapat dikendalikan melalui state, sedangkan `onChange` dan `onSubmit` digunakan untuk menangani perubahan serta pengiriman data. Untuk formulir yang lebih kompleks, Formik dapat membantu mengelola nilai, validasi, dan proses pengiriman formulir secara lebih terstruktur.
