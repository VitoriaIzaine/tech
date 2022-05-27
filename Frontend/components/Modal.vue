<template>
    <!-- <transition name="modal-fade"> -->
    <div class="modal-overlay" @click="$emit('close-modal')">
        <div class="modal" @click.stop>
            <h1>Cadastro de Equipamento</h1>
            <form class="base" method="POST">
                <input type="text" name="name" class="inputs" id="name" placeholder="name" v-model="device.name" />
                <input class="image" id="customFileUpload" type="file" @change="saveFile($event.target)"
                    accept=".png, .svg, .jpg, .jpeg" />
                <input type="text" name="desc" class="inputs" id="name" placeholder="desc"
                    v-model="device.description" />
                <input type="checkbox" id="ativo" name="ativo" value="ativo" v-model="device.status">
                <button @click.prevent="postPhoto" type="submit">Cadastrar</button>
            </form>
        </div>
    </div>
    <!-- </transition> -->
</template>

<script>
export default {
    name: 'modal',
    data() {
        return {
            device: {
                name: '',
                description: '',
                image: null,
                status: false,
            },
        }
    },
    methods: {
        saveFile: async function (event) {
            this.device.image = event.files[0];
            console.log(this.device.file)
        },
        postPhoto: async function () {
            console.log(this.device)
            console.log("xcsdsdsdsds")
            let formData = new FormData()
            formData.append('name', this.device.name)
            formData.append('description', this.device.description)
            formData.append('image', this.device.image)

            if (this.device.status) {
                formData.append('status', 'True')
            }
            else {
                formData.append('status', 'False')
            }

            console.log(formData)

            this.$axios
                .$post(this.$store.state.BASE_URL + '/devices/', formData, {
                    headers: {
                        'Content-Type': 'multipart/form-data',
                    },
                })
                .then((response) => {
                    console.log(response)
                    console.log("poo")
                })
                .catch((response) => {
                    console.log(err)
                })
        },
    },
}
</script>

<style scoped>
button {
    background: #35797d;
    padding: 0.5em 0.5em;
    border: none;
    border-radius: 7px;
    font-size: 17px;
    color: white;
    transition: all .5s ease-in-out;
    margin-top: 10%;
    width: 100%;
}

button:hover {
    animation: gradient 3s infinite;
    transform: scale(1.05);
}

.modal-overlay {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    background-color: #000000da;
}

.modal {
    color: black;
    text-align: left;
    background: #fff;
    height: 300px;
    width: 450px;
    margin-top: 10%;
    padding: 0px 60px 60px;
}

h6 {
    font-weight: 500;
    font-size: 28px;
    margin: 20px 0;
    margin-top: 10%;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
    transition: opacity 0.5s ease;
}

.customFileUpload {
    width: 70%;
    margin-left: 8px;
    border: 2px solid black;
    border-radius: 6px;
    padding: 10px;
}

.p-fileupload-buttonbar {
    border: none !important;
    border-color: #a19d9d !important;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
}

.lblBasic {
    margin: 10px 0px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
}

.pi {
    width: auto;
    margin-right: 5px;
    font-weight: bold;
}

.inputs {
    padding: 0.7em 0.7em;
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    border: 2px solid #a19d9d;
    align-items: center;
}

#nome {
    margin-top: 5%;
    width: 70%;
}

#email {
    margin-top: 2%;
    width: 70%;
}
</style>