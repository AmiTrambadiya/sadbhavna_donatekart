<template>
    <Navbar />
    <div class="container mx-auto">
        <div v-if="openTab == 1"
            class="absolute bg-bottom bg-x-center bg-y-bottom bg-no-repeat z-1 top-96 sm:h-0 md:h-0 lg:h-0 xl:h-[650px] sm:w-0 md:w-0 lg:w-0 xl:w-96  sm:right-0 md:right-5 lg:right-16 bg-no-repeat opacity-40 bg-white bg-contain bg-no-repeat"
            style="
                                                                                                                                                                                                                                                                                                                            background-image: url('../../src/assets/Inter/img/bg-tree.png');
                                                                                                                                                                                                                                                                                                                          ">
        </div>
        <div v-if="openTab == 2"
            class="absolute bg-bottom bg-x-center bg-y-bottom bg-no-repeat z-1 top-[300px] sm:h-0 md:h-0 lg:h-0 xl:h-[643px] sm:w-0 md:w-0 lg:w-0 xl:w-96  sm:right-0 md:right-5 lg:right-16 bg-no-repeat opacity-40 bg-white bg-contain bg-no-repeat"
            style="
                                                                                                                                                                                                                                                                                                                            background-image: url('../../src/assets/Inter/img/bg-tree.png');
                                                                                                                                                                                                                                                                                                                          ">
        </div>
        <div class="container mx-auto h-full">

            <div class="w-full sm:pt-0 md:pt-5 lg:pt-12">
                <div class="container mx-auto py-0">
                    <div class="w-6/6 lg:w:4/6 mx-auto bg-white">
                        <div
                            class="text-[24px] md:text-[30px] lg:text-[36px] py-8 px-10 text-gray-600 font-[200px] text-center">
                            Donation Campaign Request
                        </div>
                        <div class="relative z-0">
                            <div class=" sm:p-10 ">
                                <ul class="flex  mb-0 flex-wrap pt-4 ml-10 mr-11 pb-4 flex-row">
                                    <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
                                        <a class="cursor-pointer text-base font-bold uppercase px-5 py-3 shadow-lg rounded block leading-normal"
                                            v-on:click="toggleTabs(1)"
                                            v-bind:class="{ 'text-[#40b751] bg-white': openTab !== 1, 'text-white bg-[#40b751]': openTab === 1 }">
                                            NGO
                                        </a>
                                    </li>
                                    <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
                                        <a class="cursor-pointer text-base font-bold uppercase px-5 py-3 shadow-lg rounded block leading-normal"
                                            v-on:click="toggleTabs(2)"
                                            v-bind:class="{ 'text-[#40b751] bg-white': openTab !== 2, 'text-white bg-[#40b751]': openTab === 2 }">
                                            Individual Group
                                        </a>
                                    </li>
                                </ul>
                                <form @submit.prevent="submitForm">
                                    <div class="px-4 py-2 flex-auto form control"
                                        :class="{ invalid: fullnameValidity === 'invalid' }">
                                        <div class="tab-content tab-space">
                                            <div class="py-4 px-8">
                                                <div class="mb-4">

                                                    <label class="block text-gray-600 text-base  mb-2" for="email">Full
                                                        Name</label>
                                                    <input
                                                        class="appearance-none border-gray-300  hover:border-[#40b751] rounded w-full py-2 px-3 text-grey-darker"
                                                        v-model.trim="full_name" type="text" required>
                                                    <!-- <input
                                                        class="appearance-none border-gray-300  hover:border-[#40b751] rounded w-full py-2 px-3 text-grey-darker"
                                                        v-model.trim="full_name" type="text" @blur="validateFullname"
                                                        required>
                                                    <p class="text-red-600" v-if="fullnameValidity === 'Invalid'">Please
                                                        enter valid name</p> -->
                                                </div>
                                                <div v-if="openTab == 1"
                                                    class="grid sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-2 gap-4">
                                                    <div class="mb-4">
                                                        <label class="block text-gray-600 text-base  mb-2">Organisation
                                                            Name</label>
                                                        <input
                                                            class="appearance-none border-gray-300 rounded w-full py-2 px-3 hover:border-[#40b751] text-grey-darker"
                                                            type="text" v-model="organisation_name" required>
                                                    </div>
                                                    <div class="mb-4">
                                                        <label class="block text-gray-600 text-base  mb-2">Organisation
                                                            Website</label>
                                                        <input
                                                            class="appearance-none border-gray-300 hover:border-[#40b751] rounded w-full py-2 px-3 text-grey-darker"
                                                            type="text" v-model="organisation_website" required>
                                                    </div>
                                                </div>
                                                <div class="grid sm:grid-cols-1 md:grid-cols-1 lg:grid-cols-3 gap-4">
                                                    <div class="mb-6">
                                                        <label class="block text-gray-600 text-base  mb-2">Phone</label>
                                                        <input
                                                            class="appearance-none border-gray-300 hover:border-[#40b751] rounded w-full py-2 px-3 text-grey-darker"
                                                            type="text" v-model.trim="phone" @blur="validatePhone" required>
                                                        <p class="text-red-600">{{ phoneErrorMessage }}</p>
                                                        <!-- <p class="text-red-600" v-if="phoneValidity === 'Invalid'">Please
                                                            enter valid phone number</p> -->
                                                    </div>
                                                    <div class="mb-6">
                                                        <label class="block text-gray-600 text-base  mb-2">Email</label>
                                                        <input
                                                            class="appearance-none border-gray-300 hover:border-[#40b751] rounded w-full py-2 px-3 text-grey-darker"
                                                            type="email" v-model.trim="email" required>
                                                        <!-- <p class="text-red-600" v-if="emailValidity === 'Invalid'">Please
                                                            enter valid email</p> -->
                                                        <p class="text-red-600">{{ emailErrorMessage }}</p>
                                                    </div>
                                                    <div class="mb-6">
                                                        <label class="block text-gray-600 text-base  mb-2">Social Media
                                                            Page</label>
                                                        <input
                                                            class="appearance-none border-gray-300 hover:border-[#40b751] rounded w-full py-2 px-3 text-grey-darker"
                                                            type="text" v-model="social_media_page" required>
                                                    </div>
                                                </div>
                                                <div class="grid sm:grid-cols-1 md:grid-cols-1 lg:grid-cols-2 gap-4">
                                                    <div class="mb-6">
                                                        <label class="block text-gray-600 text-base  mb-2">Campaign
                                                            Story</label>
                                                        <textarea id="comment" rows="4" v-model="campaign_story"
                                                            class="hover:border-[#40b751] w-full py-2 px-3 text-gray-900 bg-white border-1 border-gray-300  focus:ring-0 dark:text-white dark:placeholder-gray-600"
                                                            required></textarea>
                                                    </div>
                                                    <div class="mb-6">
                                                        <label class="block text-gray-600 text-base  mb-2">Beneficiary
                                                            Group</label>
                                                        <textarea id="comment" rows="4" v-model="beneficiary_group"
                                                            class="hover:border-[#40b751] w-full py-2 px-3 text-gray-900 bg-white border-1 border-gray-300  focus:ring-0 dark:text-white dark:placeholder-gray-600"
                                                            required></textarea>
                                                    </div>
                                                </div>
                                                <div class="mb-6">
                                                    <button type="submit"
                                                        class="appearance-none border-gray-600 rounded w-full py-2 px-3 text-grey-darker bg-[#40b751] hover:bg-transparent text-white hover:text-[#40b751] py-2 tracking-wide px-4 border border-[#40b751] hover:border-[#40b751]  text-lg uppercase rounded"
                                                        @click="request_campaign()">Submit</button>
                                                </div>
                                            </div>
                                        </div>

                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <Footer />
</template>
   
<script>
import Navbar from "../components/Navbar.vue";
import Footer from "../components/Footer.vue";

export default {
    name: "Donation Campaign Request",
    components: {
        Navbar,
        Footer
    },
    data() {
        return {
            openTab: 1,
            full_name: '',
            fullnameValidity: '',
            campaign_type: '',
            organisation_name: '',
            organisation_website: '',
            email: '',
            // emailValidity: 'pending',
            phone: '',
            phoneValidity: '',
            campaign_story: '',
            social_media_page: '',
            beneficiary_group: ''
        }
    },
    watch: {
        email(value) {
            this.email = value;
            this.validateEmail(value);
        },
        phone(value) {
            this.phone = value;
            this.validatePhoneNumber(value);
        }
    },
    resources: {
        request_campaign() {
            return {
                method: 'sadbhavna_donatekart.api.campaign.request_campaign',
                onSuccess: (res) => {
                    // this.recent_donation = res
                    this.$toast({
                        title: "Success",
                        text: "Your Request is successfully sent to sadbhavna donatekart",
                        customIcon: "check",
                    })

                },
                onError: (error) => {
                    console.log(error)
                    this.$toast({
                        title: "Error",
                        text: error,
                        customIcon: "circle-fail",
                        appearance: "denger",
                    })
                }
            }
        }
    },

    methods: {
        toggleTabs: function (tabNumber) {
            this.openTab = tabNumber
            this.tab = this.tabNumber
        },
        // submitForm() {
        //     console.log('Fullname:' + this.full_name);
        //     this.full_name = '';
        // },
        // validateInput() {
        //     if (this.full_name === '') {
        //         this.fullnameValidity = 'Invalid';
        //     } else {
        //         this.fullnameValidity = 'Valid';
        //     }
        // },
        // validateEmail() {
        //     if (this.email === '') {
        //         this.emailValidity = 'Invalid';
        //     } else {
        //         this.emailValidity = 'Valid'
        //     }
        // },
        validatePhone() {
            if (this.phone === '') {
                this.phoneValidity = 'Invalid';
            } else {
                this.phoneValidity = 'Valid'
            }

        },
        validateFullname() {
            if (this.full_name === '') {
                this.fullnameValidity = 'Invalid';
            } else {
                this.fullnameValidity = 'Valid';
            }
        },
        validateEmail(email) {
            if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(email)) {
                this.emailErrorMessage = ''
            } else {
                this.emailErrorMessage = 'Invalid email!'
            }
        },
        validatePhoneNumber(phone) {
            if (/^[6-9][0-9]{9}$/.test(phone)) {
                this.phoneErrorMessage = ''
            } else {
                this.phoneErrorMessage = 'Invalid phone number!'
            }
        },
        request_campaign() {
            // console.log("opentab", this.openTab)
            if (this.openTab == 1) {
                this.campaign_type = 'NGO'
            }
            else {
                this.campaign_type = 'Indivisual/Group'
            }
            this.$resources.request_campaign.submit({
                full_name: this.full_name,
                campaign_type: this.campaign_type,
                organisation_name: this.organisation_name,
                organisation_website: this.organisation_website,
                email: this.email,
                phone: this.phone,
                campaign_story: this.campaign_story,
                social_media_page: this.social_media_page,
                beneficiary_group: this.beneficiary_group
            })

        }
    }
}
</script>

<!-- <style>
.form-control.invalid input {
    border-color: red;
}

.form-control.invalid label {
    color: red;
}
</style> -->