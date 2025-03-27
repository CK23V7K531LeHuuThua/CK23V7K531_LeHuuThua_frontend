<template>
    <div class="page">
        <h4>Thêm Mới Liên Hệ</h4>
        <ContactForm :contact="contactData" @submit:contact="createContact" :showCancel="false" />
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
            contactData: { name: "", email: "", address: "", phone: "", favorite: false },
            message: "" 
        };
    },
    methods: {
        async createContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên Hệ Mới Được Thêm Thành Công"
                setTimeout(() => {
                    this.$router.push({ name: "contactbook" });
                }, 1500);
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.message = "";
    },
};
</script>