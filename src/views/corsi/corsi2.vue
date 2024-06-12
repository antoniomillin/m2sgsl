<script setup>
import { computed, nextTick, ref, watch } from 'vue';
import axios  from 'axios';
import BaseBreadcrumb from '@/components/shared/BaseBreadcrumb.vue';
import UiParentCard from '@/components/shared/UiParentCard.vue';
const page = ref({ title: 'CRUD Table' });
const breadcrumbs = ref([
    {
        text: 'Dashboard',
        disabled: false,
        href: '#'
    },
    {
        text: 'CRUD Table',
        disabled: true,
        href: '#'
    }
]);

const dialog = ref(false)
const dialogDelete = ref(false)
const headers = ref([
    {
        title: 'Descr',
        align: 'start',
        sortable: false,
        key: 'custDescr',
    },
    { title: 'GUID', key: 'custGUID' },
    /*
    { title: 'Fat (g)', key: 'fat' },
    { title: 'Carbs (g)', key: 'carbs' },
    { title: 'Protein (g)', key: 'protein' },
    { title: 'Actions', key: 'actions', sortable: false },
    */
])
const desserts = ref([])
const editedIndex = ref(-1)
const editedItem = ref({
    custDescr: '',
    custGUID: 0,
    /*
    fat: 0,
    carbs: 0,
    protein: 0,
    */
})
const defaultItem = ref({
    custDescr: '',
    custGUID: 0,
    /*
    fat: 0,
    carbs: 0,
    protein: 0,
    */
})
const formTitle = computed(() => {
    return editedIndex.value === -1 ? 'New Item' : 'Edit Item'
})

'returnData': async function() {

const axios = require('axios').default;

try {
    return await axios.get('https://eodhistoricaldata.com/api/eod/MCD.US', {
                params: {
                  api_token: 'xxxx',
                  fmt: 'json'
                }
              }).then(content => content.data);
  } catch (error) {
    throw {
      code: error.code,
      message: error.message,
      responseStatus: error.response?.status,
      url
    };
  }

},

function initialize() {

    desserts.value = 
    
    try {
    return await axios.get(url).then(content => content.data);
  } catch (error) {
    throw {
      code: error.code,
      message: error.message,
      responseStatus: error.response?.status,
      url
    };
  }
    
    
    axios.create('https://m2sgsl-api-b0dec18fded3.herokuapp.com/customer/');
    /*
    desserts.value = [
        {
            "custId": 1,
            "custDescr": "test1",
            "custGUID": "23515819-f70b-11ee-a4e1-7e1b151d9f32",
            "_usrIdC": 1,
            "_grpIdC": 1,
            "_tsC": "2024-04-08T18:24:59.000Z",
            "_usrIdM": 0,
            "_grpIdM": null,
            "_tsM": "2024-05-13T21:04:00.000Z",
            "_deleted": 0
        },
        {
            "custId": 2,
            "custDescr": "Daem srl",
            "custGUID": "5e73cb3e-f70b-11ee-a4e1-7e1b151d9f32",
            "_usrIdC": 1,
            "_grpIdC": 1,
            "_tsC": "2024-04-08T18:36:13.000Z",
            "_usrIdM": 1,
            "_grpIdM": 1,
            "_tsM": "2024-04-08T18:36:13.000Z",
            "_deleted": 0
        },
        {
            "custId": 3,
            "custDescr": "prova",
            "custGUID": "91b2d098-115b-11ef-a4e1-7e1b151d9f32",
            "_usrIdC": 0,
            "_grpIdC": null,
            "_tsC": "2024-05-13T21:04:05.000Z",
            "_usrIdM": 0,
            "_grpIdM": null,
            "_tsM": "2024-05-13T21:04:05.000Z",
            "_deleted": 0
        }
    ]
*/
    
      
}
function editItem(item) {
    editedIndex.value = desserts.value.indexOf(item)
    editedItem.value = Object.assign({}, item)
    dialog.value = true
}
function deleteItem(item) {
    editedIndex.value = desserts.value.indexOf(item)
    editedItem.value = Object.assign({}, item)
    dialogDelete.value = true
}
function deleteItemConfirm() {
    desserts.value.splice(editedIndex.value, 1)
    closeDelete()
}
function close() {
    dialog.value = false
    nextTick(() => {
        editedItem.value = Object.assign({}, defaultItem.value)
        editedIndex.value = -1
    })
}
function closeDelete() {
    dialogDelete.value = false
    nextTick(() => {
        editedItem.value = Object.assign({}, defaultItem.value)
        editedIndex.value = -1
    })
}
function save() {
    if (editedIndex.value > -1) {
        Object.assign(desserts.value[editedIndex.value], editedItem.value)
    } else {
        desserts.value.push(editedItem.value)
    }
    close()
}
watch(dialog, val => {
    val || close()
})
watch(dialogDelete, val => {
    val || closeDelete()
})
initialize()
</script>

<template>
    <BaseBreadcrumb :title="page.title" :breadcrumbs="breadcrumbs"></BaseBreadcrumb>
    <v-row>
        <v-col cols="12">
            <UiParentCard title="Crud Table">
                <v-data-table class="border rounded-md" :headers="headers" :items="desserts" :sort-by="[{ key: 'custDescr', order: 'asc' }]">
                    <template v-slot:top>
                        <v-toolbar class="bg-lightprimary rounded-t-md" flat>
                            <v-toolbar-title>My Crud Table</v-toolbar-title>
                            <v-spacer></v-spacer>
                            <v-dialog v-model="dialog" max-width="500px">
                                <template v-slot:activator="{ props }">
                                    <v-btn color="primary"  variant="flat" dark  v-bind="props" >Add New Item</v-btn>
                                </template>
                                <v-card>
                                    <v-card-title class="pa-4 bg-secondary">
                                        <span class="text-h5">{{ formTitle }}</span>
                                    </v-card-title>

                                    <v-card-text>
                                        <v-container class="px-0">
                                            <v-row>
                                                <v-col cols="12" sm="6" md="4">
                                                    <v-text-field v-model="editedItem.custDescr"
                                                        label="Descrizione"></v-text-field>
                                                </v-col>
                                                <v-col cols="12" sm="6" md="4">
                                                    <v-text-field v-model="editedItem.custGUID"
                                                        label="GUID"></v-text-field>
                                                </v-col>
                                                <!--
                                                <v-col cols="12" sm="6" md="4">
                                                    <v-text-field v-model="editedItem.fat" label="Fat (g)"></v-text-field>
                                                </v-col>
                                                <v-col cols="12" sm="6" md="4">
                                                    <v-text-field v-model="editedItem.carbs"
                                                        label="Carbs (g)"></v-text-field>
                                                </v-col>
                                                <v-col cols="12" sm="6" md="4">
                                                    <v-text-field v-model="editedItem.protein"
                                                        label="Protein (g)"></v-text-field>
                                                </v-col>
                                                -->
                                            </v-row>
                                        </v-container>
                                    </v-card-text>

                                    <v-card-actions>
                                        <v-spacer></v-spacer>
                                        <v-btn color="error" variant="flat" dark   @click="close">
                                            Cancel
                                        </v-btn>
                                        <v-btn color="success" variant="flat" dark   @click="save">
                                            Save
                                        </v-btn>
                                    </v-card-actions>
                                </v-card>
                            </v-dialog>
                            <v-dialog v-model="dialogDelete" max-width="500px">
                                <v-card>
                                    <v-card-title class="text-h5 text-center py-6">Are you sure you want to delete this item?</v-card-title>
                                    <v-card-actions>
                                        <v-spacer></v-spacer>
                                        <v-btn color="error" variant="flat" dark   @click="closeDelete">Cancel</v-btn>
                                        <v-btn color="success" variant="flat" dark   @click="deleteItemConfirm">OK</v-btn>
                                        <v-spacer></v-spacer>
                                    </v-card-actions>
                                </v-card>
                            </v-dialog>
                        </v-toolbar>
                    </template>
                    <template v-slot:item.actions="{ item }">
                        <v-icon color="info" size="small" class="me-2" @click="editItem(item)">
                            mdi-pencil
                        </v-icon>
                        <v-icon color="error" size="small" @click="deleteItem(item)">
                            mdi-delete
                        </v-icon>
                    </template>
                    <template v-slot:no-data>
                        <v-btn color="primary" @click="initialize">
                            Reset
                        </v-btn>
                    </template>
                </v-data-table>
            </UiParentCard>
        </v-col>
    </v-row>
</template>
  
  