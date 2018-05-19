<template>
    <div v-if="showModal">
        <transition>
            <div class="modal-mask">
                <div class="modal-wrapper">
                    <div class="modal-container">
                        <div class="modal-header">
                            {{ title }}
                        </div>

                        <div class="modal-body">
                            <slot name="body">
                                default body
                            </slot>
                        </div>

                        <div class="modal-footer">
                            <slot name="footer">
                                default footer
                                <button class="modal-default-button" @click="closedialog">
                                    OK
                                </button>
                            </slot>
                        </div>
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
    export default {
        props:['show', 'title'],
        data () {
            return {
                showModal: this.show
            }
        },
        watch: {
            show() {
                this.showModal = this.show;
            },
        },
        methods:{
            closedialog(){
                this.showModal = false;
                this.$emit('close');
            }  
        }
    }
</script>
