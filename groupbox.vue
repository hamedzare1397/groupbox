<template>
    <v-item-group :multiple="multiple" v-model="modelVal" @update:modelValue="valUpdate">
            <v-row>
                <v-col
                    v-for="(item,index) in items"
                    :key="index"
                    :cols="cols"
                    :sm="sm"
                    :md="md"
                    :lg="lg"
                >
                    <v-item v-slot="{ isSelected, toggle }"  :value="value?item[value]:item">
                        <v-card
                            :color="isSelected ? colorSelected : ''"
                            :height="itemHeight"
                            class="d-flex justify-center align-center"
                            @click="toggle"
                        >
                            <v-scroll-y-transition>
                                <div>

                                    <span v-if="item.icon" ><v-icon :icon="item.icon" :size="iconSize"></v-icon></span>
                                    <span v-if="item[title]">{{ item[title] }}</span>
                                    <v-icon v-if="isSelected">mdi-check</v-icon>
                                </div>
                            </v-scroll-y-transition>
                        </v-card>
                    </v-item>
                </v-col>
            </v-row>
    </v-item-group>
</template>

<script setup>
import {ref,defineProps,defineEmits} from "vue";

const props=defineProps({
    colorSelected:{
        default:'primary'
    },
    iconSize:{
        default:100,
    },
    value:{
        type:String,
        default:'title',
    },
    title:{
        default:'title',
    },
    items:{
        type:Array,
        required:true,
    },
    modelValue:{
        type:Object,
    },
    multiple:{
        default:false,
        type:Boolean
    },
    itemHeight:{
        default:"25px",
        type:String
    },
    sm:{
        default:null,
        type:Number,
    },
    md:{
        default:null,
        type:Number,
    },
    cols:{
        default:12,
        type:Number,
    },
    lg:{
        default:null,
        type:Number,
    }
});
const emit=defineEmits(['update:modelValue'])
const modelVal=ref(props.modelValue)
function valUpdate(event){
    emit('update:modelValue', event);
}
</script>

<style scoped>

</style>