<template>
    <div>
        <v-card
        v-if="showWadir"
        class=" pa-6 mt-4"
        outlined
        tile
        >
            <v-card elevation="3" class="pa-8">
                <v-form ref="form" v-model="valid"  lazy-validation>

                    <v-text-field
                    outlined
                    v-model="perihal"
                    :rules="perihalRules"
                    prefix="Rapat - "
                    label="Perihal"
                    required
                    >
                    </v-text-field>

                    <v-text-field
                    outlined
                    v-model="tempat"
                    :rules="tempatRules"
                    label="Tempat"
                    required
                    ></v-text-field>
                    
                    <v-row>
                        <v-col
                            cols="12"
                            sm="6"
                            md="6"
                            >
                                <v-dialog
                                    ref="dialog1"
                                    v-model="modal"
                                    :return-value.sync="tanggal"
                                    :value="computedDateFormattedMomentjs"
                                    persistent
                                    width="290px"
                                >
                                    <template v-slot:activator="{ on, attrs }">
                                        <v-text-field
                                            v-model="tanggal"
                                            outlined
                                            label="Tanggal"
                                            prepend-icon="mdi-calendar"
                                            :rules="tanggalRules"
                                            :value="computedDateFormattedMomentjs"
                                            readonly
                                            v-bind="attrs"
                                            v-on="on"
                                        ></v-text-field>
                                    </template>
                                    <v-date-picker
                                        v-model="tanggal"
                                        scrollable
                                        @change="triple"
                                    >
                                        <v-spacer></v-spacer>
                                        <v-btn
                                            text
                                            color="primary"
                                            @click="modal = false"
                                        >
                                            Cancel
                                        </v-btn>
                                        <v-btn
                                            text
                                            color="primary"
                                            @click="$refs.dialog1.save(tanggal); alerts = true;"
                                        >
                                            OK
                                        </v-btn>
                                    </v-date-picker>
                                </v-dialog>
                        </v-col>
                        <v-col
                            cols="12"
                            sm="6"
                            md="6"
                        >
                            <v-dialog
                                ref="dialog2"
                                v-model="modal2"
                                :return-value.sync="waktu"
                                persistent
                                width="290px"
                            >
                                <template v-slot:activator="{ on, attrs }">
                                    <v-text-field
                                        v-model="waktu"
                                        outlined
                                        label="Waktu"
                                        prepend-icon="mdi-clock-time-four-outline"
                                        :rules="waktuRules"
                                        readonly
                                        v-bind="attrs"
                                        v-on="on"
                                    ></v-text-field>
                                </template>
                                <v-time-picker
                                    v-if="modal2"
                                    v-model="waktu"
                                    full-width
                                    @change="timedi"
                                >
                                    <v-spacer></v-spacer>
                                    <v-btn
                                        text
                                        color="primary"
                                        @click="modal2 = false"
                                    >
                                        Cancel
                                    </v-btn>
                                    <v-btn
                                        text
                                        color="primary"
                                        @click="$refs.dialog2.save(waktu)"
                                    >
                                        OK
                                    </v-btn>
                                </v-time-picker>
                            </v-dialog>
                        </v-col>
                    </v-row>

                    <v-alert
                    :value="alerts"
                    outlined
                    color="cyan"
                    border="left"
                    type="info"
                    transition="scale-transition"
                    >
                        <v-row>

                        <v-col
                        v-if="(fixDateCheck.length === 0)"
                        >
                            <p class="black--text">
                            Belum ada yang mengajukan hari yang dipilih. Anda bisa mengajukan rapat!!.
                            </p>
                            <v-data-table
                            :headers="headers"
                            :items="fixDateCheck"
                            sort-by="waktu"
                            class="elevation-1"
                            >
                            <template v-slot:[getItemTanggal()]="{ item }">
                                <span>{{ new Date(item.tanggal).toLocaleDateString('da') }}</span>
                                <!-- da-DK -->
                            </template>
                            </v-data-table>
                            <p class="red--text pt-6">
                            <i>
                                Catatans : Rapat maksimal dalam 1 hari adalah 3 kali dan Jika ada waktu yang sudah dipesan. Anda tidak akan bisa memilih waktu dengan jangkauan 2 jam sebelumnya dan 2 jam setelahnya !!!. Terima kasih.
                            </i>
                            </p>
                        </v-col>

                        <v-col
                        v-if="(fixDateCheck.length >= 3)"
                        >
                            <p class="red--text">
                            Hari yang dipilih sudah penuh. Mohon ma'af, tidak bisa mengajukan rapat!!.
                            <br>Berikut detail rapat yang sudah ada :
                            </p>
                            <v-data-table
                            :headers="headers"
                            :items="fixDateCheck"
                            sort-by="waktu"
                            class="elevation-1"
                            >
                            <template v-slot:[getItemTanggal()]="{ item }">
                                <span>{{ new Date(item.tanggal).toLocaleDateString('da') }}</span>
                                <!-- da-DK -->
                            </template>
                            </v-data-table>
                            <p class="red--text pt-6">
                            <i>
                                Catatans : Rapat maksimal dalam 1 hari adalah 3 kali dan Jika ada waktu yang sudah dipesan. Anda tidak akan bisa memilih waktu dengan jangkauan 2 jam sebelumnya dan 2 jam setelahnya !!!. Terima kasih.
                            </i>
                            </p>
                        </v-col>
                        
                        <v-col
                        v-if="(fixDateCheck.length >= 1 && fixDateCheck.length < 3)"
                        >
                            <p class="black--text">
                            Masih bisa mengajukan hari yang dipilih. Anda bisa mengajukan rapat!!.
                            <br>Berikut detail rapat yang sudah ada :
                            </p>
                            <v-data-table
                            :headers="headers"
                            :items="fixDateCheck"
                            sort-by="waktu"
                            class="elevation-1"
                            >
                            <template v-slot:[getItemTanggal()]="{ item }">
                                <span>{{ new Date(item.tanggal).toLocaleDateString('da') }}</span>
                                <!-- da-DK -->
                            </template>
                            </v-data-table>
                            
                            <p class="red--text pt-6">
                            <i>
                                Catatans : Rapat maksimal dalam 1 hari adalah 3 kali dan Jika ada waktu yang sudah dipesan. Anda tidak akan bisa memilih waktu dengan jangkauan 2 jam sebelumnya dan 2 jam setelahnya !!!. Terima kasih.
                            </i>
                            </p>
                        </v-col>

                        <v-divider vertical></v-divider>
                        <v-btn
                        color="red"
                        icon
                        dark
                        @click="alerts = false"
                        >
                            <v-icon>mdi-close</v-icon>
                        </v-btn>
                        </v-row>
                    </v-alert>
                    
                    <v-autocomplete
                        v-model="participants"
                        :items="people"
                        :rules="participantsRules"
                        outlined
                        chips
                        color="blue-grey lighten-2"
                        label="Peserta"
                        item-text="username"
                        item-value="username"
                        multiple
                        clearable
                        single-line
                        required
                        >
                        <template v-slot:prepend-item>
                            <v-list-item ripple @mousedown.prevent @click="toggle">
                              <v-list-item-action>
                                <v-icon
                                  :color="participants.length > 0 ? 'indigo darken-4' : ''"
                                >
                                  {{ icon }}
                                </v-icon>
                              </v-list-item-action>
                              <v-list-item-content>
                                <v-list-item-title> Select All </v-list-item-title>
                              </v-list-item-content>
                            </v-list-item>
                            <v-divider class="mt-2"></v-divider>
                          </template>
                          <template v-slot:selection="data">
                            <v-chip
                            v-bind="data.attrs"
                            :input-value="data.selected"
                            color="yellow"
                            @click="data.select"
                            >
                                {{ data.item.username }}
                            </v-chip>
                        </template>
                    </v-autocomplete>

                    <v-textarea
                    outlined
                    name="input-7-4"
                    v-model="deskripsi"
                    label="Agenda"
                    :rules="deskripsiRules"
                    required
                    ></v-textarea>

                    <v-checkbox
                    v-model="checkbox"
                    :rules="checkboxRules"
                    label="Do you agree?"
                    required
                    ></v-checkbox>


                    <v-dialog
                    v-model="dialog"
                    max-width="50rem"
                    transition="dialog-bottom-transition"
                    persistent
                    >
                        <v-card>
                            <v-toolbar
                            color="primary"
                            dark
                            >
                            <h2 v-if="success">Rapat berhasil disimpan</h2>
                            <h2 v-if="!success">Rapat gagal tersimpan</h2>
                            </v-toolbar>
                            <v-card-text>
                            <div class="text pa-12">
                                <h2 v-if="success">Anda bisa memeriksa di Data Rapat, klik dibawah ini :</h2>
                                <h2 v-if="!success">
                                    <v-alert
                                    dense
                                    outlined
                                    type="error"
                                    transition="scale-transition"
                                    class="pb-6"
                                    >
                                      <h3><strong>Pemberitahuan !!!</strong></h3>
                                      <br><i>Mohon ma'af. Pengajuan rapat sudah dipesan.</i> 
                                    </v-alert>
                                    <br><strong>Anda bisa mencoba membuat rapat lagi, klik dibawah ini :</strong>
                                  </h2>
                                </div>
                            </v-card-text>
                            <v-card-actions v-if="!success" class="justify-end">
                            <v-btn
                                class="white--text"
                                color="bg-gradient-info"
                                @click="dialog = !dialog"
                            >Close</v-btn>
                            </v-card-actions>
                            <v-card-actions v-if="success" class="justify-end">
                            <v-btn
                                class="white--text"
                                color="bg-gradient-info"
                                @click="closeDialog"
                                :to="`/user/wadir/Jadwal`"
                            >Lihat</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-dialog>
                    <v-btn
                    :disabled="!valid"
                    class="white--text mr-4 mt-4"
                    color="bg-gradient-info"
                    @click="validate"
                    >
                    submit
                    </v-btn>
                    <v-btn 
                    class="white--text mt-4"
                    color="bg-gradient-secondary"
                    @click="clear"
                    >
                    clear
                    </v-btn>
                </v-form>
            </v-card>
        </v-card>
        <v-card v-if="!showWadir" class="pa-6 mt-4" outlined tile>
            <v-card elevation="3" class="pa-8">
                <v-alert
                type="error"
                prominent
                border="left"
                >          
                <h2>Required role wadir !!!.</h2>
                </v-alert>
            </v-card>
        </v-card>
    </div>
</template>
<script>
    import moment from 'moment'
    import 'moment/locale/id'

    export default {
        data: () => ({     
            modal: false,
            modal2: false,
            dialog: false,
            alerts: false,
            checkbox: false,
            enabled: false,
            editItem : {},
                perihal: '',
                tempat: '',
                tanggal: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
                waktu: '',
                status: '2',
                participants: [],
                deskripsi: '',
                // user_id: '',
                headers: [
                    { text: "Kepeda", value: "receiver" },
                    { text: "Perihal", value: "perihal" },
                    { text: "Tempat", value: "tempat" },
                    { text: "Tanggal", value: "tanggal" },
                    { text: "Waktu", value: "waktu" },
                ],
                people: [
                    // { header: 'Tambah peserta rapat' },
                    { 
                        
                        "id": "4" ,
                        "username": "Sandra Adams" 
                    },
                ],

                people2: [{}],
      
                dateCheck: [{}],

                fixDateCheck: [{}],

                fixTimeCheck: [{}],
            
            isOperationsSuccess: false,
            valid: false,

            perihalRules : [
                v => !!v || 'Perihal is required',
                v => (v && v.length <= 30) || 'Perihal must be less than 30 characters',
                v => (v && v.length >= 4) || 'Perihal must be more than 4 characters',
            ],
            tempatRules : [
                v => !!v || 'Tempat is required',
                v => (v && v.length >= 4) || 'Tempat must be more than 4 characters',
            ],
            tanggalRules : [
                v => !!v || 'Tanggal is required',
            ],
            waktuRules : [
                v => !!v || 'Waktu is required',
            ],
            participantsRules: [
                v => !!v || 'Peserta is required',
                v => (v && v.length > 0) || 'Peserta is required'
            ],
            deskripsiRules : [
                v => !!v || 'Deskripsi is required',
                v => (v && v.length <= 250) || 'Deskripsi must be less than 250 characters',
                v => (v && v.length >= 4) || 'Deskripsi must be more than 4 characters',
            ],
            checkboxRules : [
                $v => !!$v || 'You must agree to continue!'
            ]
        }),
        computed: {
            currentUser () {
                return this.$store.state.authentication.user;
            },
            showWadir(){
                if (this.currentUser && this.currentUser.roles) {
                    return this.currentUser.roles.includes('ROLE_WADIR')
                }

                return false;
            },
            computedDateFormattedMomentjs () {
                return this.tanggal ? moment.utc(this.tanggal).format('dddd, MMMM Do YYYY') : ''
            },
            success () {
                return  this.isOperationsSuccess
            },
            likeAllParticipants () {
                return this.participants.length === this.people.length
            },
            likeSomeParticipants () {
                return this.participants.length > 0 && !this.likeAllParticipants
            },
            icon () {
                if (this.likeAllParticipants) return 'mdi-close-box'  
                if (this.likeSomeParticipants) return 'mdi-minus-box'
                return 'mdi-checkbox-blank-outline'
            }
        },
        methods: {
            async validate () {
                this.$refs.form.validate()
                if(this.$refs.form.validate()){
                    // const data = this.editItem;
                    // console.log(data);
                    let finalParticipants = this.participants;
                    if(this.isSelectAll){

                    finalParticipants = finalParticipants.filter(item=> item != undefined).map((item) => item.username)
                    }
                    const nameUser = this.$store.state.authentication.user.username;
                    const position = this.$store.state.authentication.user.position
                    await this.$axios({
                        // withCredentials:true,
                        method: 'post',
                        url: '/meet/submission',
                        data: {
                            perihal: 'Rapat ' + this.perihal,
                            tempat: this.tempat,
                            tanggal: this.tanggal,
                            waktu: this.waktu,
                            status: this.status,
                            receiver: position,
                            participants: finalParticipants,
                            deskripsi: this.deskripsi,
                            user_id: JSON.stringify(this.$store.state.authentication.user.id),
                            maker: nameUser,
                        }
                    }).then(response => {
                        this.isOperationsSuccess = true
                        this.dialog = true
                        console.log(response.data)
                    })
                    .catch(e => {
                        this.isOperationsSuccess = false
                        this.dialog = true
                        console.log(e, 'error')
                        console.log(e.response.data.message)
                    })
                }
            },
            async getMeet() {
                const getData = await this.$axios(
                    `/meet/process-and-success`
                );
                this.dateCheck = getData.data;
            
            },
            async getParticipants (){
                const username  = this.$store.state.authentication.user.username;
                const getData = await this.$axios(`/api/auth/user-invite/${username}`);
                this.people = getData.data;
                this.people2 = getData.data;
            },
            getItemTanggal() {
                return "item.tanggal";
            },
            clear () {
                this.$refs.form.reset()
            },
            remove (item) {
                const index = this.participants.indexOf(item.username)
                if (index >= 0) this.participants.splice(index, 1)
            },
            triple() {
            const triplying = this.dateCheck.filter((item) => {
                return moment(item.tanggal).isSame(new Date(this.tanggal), "day")
                })
                if(triplying.length >= 3) {
                    console.log("error")
                } else {
                    console.log('betul')
                }
                this.fixDateCheck = triplying;
                this.fixUnvalaibleParticipantsCheck = []
                this.fixUnvalaibleParticipantsCheck = this.fixDateCheck.map(item => item.participants).flat(1)
                const res = this.people2.filter(item => !this.fixUnvalaibleParticipantsCheck.includes(item.username))
                this.people = res
            },
            timedi() {
                const timede = this.dateCheck.filter((item) => {
                return moment(item.tanggal).isSame(new Date(this.tanggal), "day")
                }).filter((item)=> {
                    var format = 'HH:mm'
                    const time = moment(this.waktu, format);
                    const beforeTime = moment(item.waktu, format).add(-2, 'hours');
                    const afterTime = moment(item.waktu, format).add(2, 'hours');
                    // console.log(time, beforeTime, afterTime)
                    if(time.isBetween(beforeTime, afterTime)) {
                        console.log('tidak boleh')
                    }
                })
                this.fixTimeCheck = timede;
            },
            closeDialog() {
                this.$refs.form.reset();
                this.dialog = false;
                this.alerts = false;
            },
            toggle () {
                this.$nextTick(() => {
                    this.participants = this.people;
                    this.isSelectAll = true;
                });
            }
        },
        mounted() {
            this.getParticipants();
            this.getMeet();
            if (!this.currentUser) {
                this.$router.push('/');
            }
        },
    }
</script>
<style>
    
</style>