<template>

<div>
    <div class="p-3 bg-white border-b flex flex-row shadow-md mb-2">
        <h1 class="text-2xl italic">{{ judulNavbar }}</h1>
        <router-link class="p-2 bg-blue-600 text-white w-auto text-sm ml-4" :to="{name: 'CIFAdd'}">Tambah CIF baru</router-link>
    </div>
    <div class="p-2">
        <div>
            <table class="border border-white w-full shadow-md">
                <thead class="bg-slate-500 text-white">
                    <tr>
                        <th class="p-4 bold font-md text-left font-semibold w-[50px]">No.#</th>
                        <th class="p-4 bold font-md text-left font-semibold">No. Kode Identitas</th>
                        <th class="p-4 bold font-md text-left font-semibold">Nama Nasabah</th>
                        <th class="p-4 bold font-md text-left font-semibold">Tanggal Ditambahkan</th>
                        <th class="p-4 bold font-md text-center font-semibold">Aksi</th>
                    </tr>
                </thead>
                <tbody class="bg-white">
                    <tr v-for="(dat, index) in isiTabelCIF" :key="dat.cif_kode_id" class="even:bg-slate-200 even:text-black">
                        <td class="border border-white text-center p-3">{{ index + 1 }}</td>
                        <td class="border border-white p-3">{{ dat.kd_identitas }}</td>
                        <td class="border border-white p-3">{{ dat.nama_sesuai_identitas }}</td>
                        <td class="border border-white p-3">{{ convertTanggal(dat.created_at) }}</td>
                        <td class="border border-white p-3 text-center"><router-link :to="{ name: 'CIFDetail', query: { id: dat.id } }" class="p-2 text-white bg-blue-600 w-auto text-sm ml-4">Details</router-link></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

</div>
</template>

<script>
import axios from 'axios'


export default {
    mounted() {
        axios.get('/api/bank/listCIF').then(res => {
            this.isiTabelCIF = res.data.data
            console.log(this.isiTabelCIF)
        })
    },
    data() {
        return {
            judulNavbar     : 'Customer Identification File',
            isiTabelCIF     : [],
            openModalAddCIF : false,
            formTambahCIF   : {
                jenisIdentitas      : '',
                kodeIdentitas       : '',
                namaIdentitas       : '',
                tempatLahir         : '',
                tanggalLahir        : '',
                jenisKelamin        : '',
                statusKawin         : '',
                warganegara         : '',
                alamatSekarang      : '',
                rtRw                : '',
                desaKelurahan       : '',
                kecamatan           : '',
                kabKota             : '',
                provinsi            : '',
                kodePos             : '',
                noTelp              : '',
                eMail               : '',
                namaEmak            : '',
                statusKerja         : '',
                modalStatus         : false
            },
        }
    },
    methods: {
        convertTanggal(initanggal) {
            var tanggal = new Date(initanggal)
            return tanggal.toLocaleDateString('id-ID', {year: 'numeric', month: 'long', day: 'numeric'})
        }
    }
}
</script>