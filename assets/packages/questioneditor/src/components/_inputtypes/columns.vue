<script>
    import abstractBaseType from '../abstracts/_abstractInputType';
    export default {
        name: 'setting-columns',
        extends: abstractBaseType,
        /*
        Abstract base provides props: 
         - elId
         - elName
         - elLabel
         - elHelp
         - currentValue
         - elOptions
         - readonly
         - debug
        */
        /*
        Abstract base provides data: 
         - triggerShowHelp
        */
        computed: {
            /*
            Abstract base provides computed values: 
             - curValue
             - getClasses
             - showHelp
             - hasPrefix
             - hasSuffix
            */
            curValue: {
                get() { return this.currentValue || this.elOptions.default || '' },
                set(newValue) {
                    this.$emit('change', newValue);
                },
            },
        }
    };
</script>

<template>
    <div class="form-row">
        <i
                class="fa fa-question pull-right"
                @click="triggerShowHelp=!triggerShowHelp"
                v-if="(elHelp.length>0) && !readonly"
                :aria-expanded="!triggerShowHelp"
                :aria-controls="'help-'+(elName || elId)"
        />
        <label class="form-label" :for="elId"> {{elLabel}} </label>
        <div class="input-group col-12">
            <div v-if="hasPrefix" class="input-group-addon"> {{elOptions.inputGroup.prefix}} </div>
            <input
                    type="number"
                    v-model="curValue"
                    :class="getClasses"
                    :name="elName || elId"
                    :id="elId"
                    :max="12"
                    :min="1"
                    :readonly="readonly"
            />
            <div v-if="hasSuffix" class="input-group-addon"> {{elOptions.inputGroup.suffix}} </div>
        </div>
        <transition name="fade">
            <div
                    class="question-option-help well"
                    :id="'help-'+(elName || elId)"
                    v-show="showHelp"
                    v-html="elHelp"
            />
        </transition>
    </div>
</template>