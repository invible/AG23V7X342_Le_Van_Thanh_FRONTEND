<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="addContact"/>
        <p>{{ message }}</p>
    </div>
</template>
<script>
    import ContactForm from "@/components/ContactForm.vue";
    import ContactService from "@/services/contact.service";
    export default {
        components: {
            ContactForm,
        },
        data() {
            return {
                // Khởi tạo contact rỗng để hiển thị form
                contact: {
                    name: "",
                    email: "",
                    address: "",
                    phone: "",
                    favorite: false,
                },
                message: "",
            };
        },
        methods: {
            async addContact(data) {
                try {
                    await ContactService.create(data);
                    alert('Liên hệ được thêm mới thành công.');
                    this.$router.push({ name: "contactbook" });
                } catch (error) {
                    console.log(error);
                }
            },
        },
    };
</script>