<script setup>

const props = defineProps({
    isOpen: Boolean
});

const emit = defineEmits(["modal-close"]);

const target = ref(null);

onClickOutside(target, () => emit('modal-close'));

</script>

<template>
    <!-- Modal -->
    <div v-if="isOpen" class="modal fade" tabindex="-1" aria-labelledby="formModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="formModalLabel">Modal title</h5>
                    <button type="button" class="btn-close" aria-label="Close" @click.stop="emit('modal-close')"></button>
                </div>
                <div class="modal-body">
                    <div class="mb-3">
                        <label for="">Name</label>
                        <input v-model="model.student.product_name" type="text" class="form-control" />
                    </div>
                    <div class="mb-3">
                        <label for="">Desc</label>
                        <input v-model="model.student.description" type="text" class="form-control" />
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button type="button" @click="updateStudent" class="btn btn-primary">Save changes</button>
                </div>
            </div>
        </div>
    </div>
</template>