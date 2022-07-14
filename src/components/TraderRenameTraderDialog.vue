<template>
    <v-dialog v-model="dialog" width="500">
        <v-card>
            <v-card-title>Rename Trader</v-card-title>
            <v-card-subtitle>Rename a Trader</v-card-subtitle>
            <v-divider class="mb-5"></v-divider>

            <v-card-text>
                <v-text-field
                    label="Trader Name"
                    filled
                    clearable
                    hint="This will appear in your Trader menu."
                    required
                    v-model='traderName'
                />
            </v-card-text>

            <v-card-actions class="d-flex flex-row flex-justify-right">
                <v-btn depressed class="flex-grow-1" @click='dialog = false'>Cancel</v-btn>
                <v-btn depressed class="flex-grow-1" @click='renameTrader' color="primary">Rename</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
export default {
    name: 'TraderRenameTraderDialog',

    props: {
        showDialog: Boolean,
        oldName: String,
        typeId: String
    },

    data() {
        return {
            traderName: ''
        }
    },

    watch: {
        showDialog: function(val) {
            if (val) {
                this.traderName = this.oldName.trim();
            }
        }
    },

    computed: {
        dialog: {
            get: function() {
                return this.showDialog
            },
            set: function(val) {
                this.$emit('update:showDialog', val);
            }
        }
    },

    methods: {

        /**
         * Rename a trader
         */
        renameTrader()
        {
            this.dialog = false;

            this.$store.state.traderModule.traderConfig.renameTrader(this.typeId, this.traderName);
        }
    }
}
</script>