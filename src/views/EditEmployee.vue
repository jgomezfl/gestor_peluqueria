<template>

    <div v-if="isAdmin">
        <div v-if="listo">
            <div  v-if="pantallaGrande" class="container mt-5">
                <div class="row justify-content-center">
                    <div class="col-md-auto card">
                        <div class="card-body p-1">

                            <div v-if="!previewImage"
                             class="imagePreviewWrapper"
                             style="margin-right: auto; margin-left: auto;"
                             :style="[photoURL ? { 'background-image': `url(${photoURL})`} :  { 'background-image': `url(${require('../assets/icono.png')})`}]"
                             @click="selectImage"></div>

                            <div
                             class="imagePreviewWrapper"
                             v-if="previewImage"
                             style="margin-right: auto; margin-left: auto;"
                             :style="{ 'background-image': `url(${previewImage})` }"
                             @click="selectImage"></div>

                            <h4 class="text-uppercase text-center">{{ empleado.rol }}</h4>

                            <input
                             ref="fileInput"
                             type="file"
                             style="margin-right: auto; margin-left: auto;"
                             class="invisible"
                             @input="pickFile"
                             accept="image/*"/>

                            

                            <div class="border my-4">
                                <h3 class="my-3">Información Personal</h3>

                                <div class="d-flex flex-wrap justify-content-center my-3 align-items-center">

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Nombres Completos</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="30"
                                         v-model="empleado.nombres"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Apellidos Completos</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="30"
                                         v-model="empleado.apellidos"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Fecha de Ingreso</h6>
                                        <input 
                                         type="date"
                                         id="startDate"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="30"
                                         v-model="empleado.fechaContracion"/>
                                    </div>

                                </div>

                                <div class="d-flex flex-wrap justify-content-around my-3">

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Tipo de Identificación</h6>
                                        <select class="form-select border-0 formato-inputs"
                                         v-model="empleado.tipoIdentificacion">
                                            <option value="cc">Cedula</option>
                                            <option value="ti">Tarjeta de identidad</option>
                                            <option value="pp">Pasaporte</option>
                                            <option value="ppt">PPT</option>
                                        </select>
                                    </div>

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Número de Identificación</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         pattern="\d*"
                                         maxlength="20"
                                         v-model="empleado.NoIdentificacion"/>
                                    </div>

                                </div>

                                <div class="d-flex mt-2 flex-wrap justify-content-around my-3">

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Fecha de Nacimiento</h6>
                                        <input 
                                         type="date"
                                         id="startDate"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="30"
                                         v-model="empleado.fechaNacimiento"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Lugar de Nacimiento</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="30"
                                         v-model="empleado.LugarNacimiento"/>
                                    </div>
                                
                                </div>

                                <div class="d-flex mt-2 flex-wrap justify-content-center my-3">

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Dirección de Residencia</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="40"
                                         v-model="empleado.direccion"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Número Telefonico</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         pattern="\d*"
                                         maxlength="15"
                                         v-model="empleado.celular"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja" style="width: 300px;">
                                        <h6 class="border-bottom">Correo Electrónico</h6>
                                        <input 
                                         type="text"
                                         style="width: 290px;"
                                         placeholder="ejemplo@gmail.com" 
                                         class="form-control border-0 formato-inputs"
                                         maxlength="40"
                                         v-model="empleado.correo"/>
                                    </div>

                                </div>

                            </div>

                            <div class="border my-2">
                                <h3 class="my-3">Información de Contacto</h3>
                                <div class="mt-1 d-flex flex-wrap justify-content-around my-3">

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Nombres Completos</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="30"
                                         v-model="contacto.nombres"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Apellidos Completos</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="30"
                                         v-model="contacto.apellidos"/>
                                    </div>

                                </div>

                                <div class="d-flex mt-2 flex-wrap justify-content-center my-3">

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Dirección de Residencia</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         maxlength="40"
                                         v-model="contacto.direccion"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja">
                                        <h6 class="border-bottom">Número Telefonico</h6>
                                        <input 
                                         type="text"
                                         class="form-control border-0 formato-inputs"
                                         pattern="\d*"
                                         maxlength="15"
                                         v-model="contacto.numero"/>
                                    </div>

                                    <div class="p-1 border mx-2 caja" style="width: 300px;">
                                        <h6 class="border-bottom">Correo Electrónico</h6>
                                        <input 
                                         type="text"
                                         style="width: 290px;"
                                         placeholder="ejemplo@gmail.com" 
                                         class="form-control border-0 formato-inputs"
                                         maxlength="40"
                                         v-model="contacto.correo"/>
                                    </div>
                            
                                </div>
                            </div>

                            <div class="d-flex flex-wrap justify-content-around">

                                <button class="boton_cancelar px-5 py-1 border my-3" v-on:click="cancelarBoton">
                                    <h5>Cancelar</h5>
                                </button>

                                <button class="boton_cancelar px-5 py-1 border my-3" v-on:click="eliminarUsuario">
                                    <h5>Eliminar</h5>
                                    <!-- <i class="fa-solid fa-eraser"></i> -->
                                </button>

                                <button class="boton px-5 py-1 border my-3" v-on:click="submitForm">
                                    <h5>Guardar</h5>
                                </button>

                            </div>

                        </div>
                    </div>
                </div>
            </div>

            <div v-else class="editar_pp">
                <div class="d-flex justify-content-center">
                    <div class="card">
                        <div class="card-body p-1 border">
                            <div v-if="!previewImage" 
                             class="imagePreviewWrapper"
                             style="margin-right: auto; margin-left: auto;"
                             :style="[photoURL ? { 'background-image': `url(${photoURL})`} :  { 'background-image': `url(${require('../assets/icono.png')})`}]"
                             @click="selectImage"></div>

                            <div v-if="previewImage"
                             class="imagePreviewWrapper"
                             style="margin-right: auto; margin-left: auto;"
                             :style="{ 'background-image': `url(${previewImage})` }"
                             @click="selectImage"></div>

                            <h6 class="text-uppercase text-center">{{ empleado.rol }}</h6>

                            <input
                             ref="fileInput"
                             type="file"
                             style="margin-right: auto; margin-left: auto;"
                             class="invisible"
                             @input="pickFile"
                             accept="image/*"/>
                            
                            <div class="border my-4 p-1">
                                <h6 class="my-2">Información Personal</h6>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Nombres Completos</p>
                                    <input type="text"
                                     class="form-control border-0 mt-0 formato-inputs"
                                     maxlength="30"
                                     v-model="empleado.nombres"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Apellidos Completos</p>
                                    <input type="text"
                                     class="form-control border-0 mt-0 formato-inputs"
                                     maxlength="30"
                                     v-model="empleado.apellidos"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Fecha de Ingreso</p>
                                    <input type="date"
                                    class="form-control border-0 mt-0"
                                    id="startDate"
                                    v-model="empleado.fechaContracion"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Tipo de Identificación</p>
                                    <select class="form-select border-0" aria-label="Default select example"
                                    v-model="empleado.tipoIdentificacion">
                                    <option value="cc">Cedula</option>
                                    <option value="ti">Tarje de Identidad</option>
                                    <option value="pp">Pasaporte</option>
                                    <option value="ppt">PPT</option>
                                    </select>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Número de Identificación</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0"
                                    pattern="\d*"
                                    maxlength="20"
                                    v-model="empleado.NoIdentificacion"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Fecha de Nacimiento</p>
                                    <input type="date"
                                    class="form-control border-0 mt-0"
                                    id="startDate"
                                    v-model="empleado.fechaNacimiento"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Lugar de Nacimiento</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0 formato-inputs"
                                    maxlength="30"
                                    v-model="empleado.LugarNacimiento"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Dirección de Residencia</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0 formato-inputs"
                                    maxlength="40"
                                    v-model="empleado.direccion"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Número de Celular</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0"
                                    pattern="\d*"
                                    maxlength="20"
                                    v-model="empleado.celular"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Correo Electrónico</p>
                                    <input type="text"
                                    placeholder="ejemplo@gmail.com"
                                    class="form-control border-0 mt-0 formato-inputs"
                                    maxlength="40"
                                    v-model="empleado.correo"/>
                                </div>
                            </div>
                            <div class="border my-4 p-1">
                                <h4 class="my-2">Información de Contacto</h4>
                                
                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Nombres Completos</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0 formato-inputs"
                                    maxlength="30"
                                    v-model="contacto.nombres"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Apellidos Completos</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0 formato-inputs"
                                    maxlength="30"
                                    v-model="contacto.apellidos"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Dirección de Residencia</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0 formato-inputs"
                                    maxlength="40"
                                    v-model="contacto.direccion"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Número de Celular</p>
                                    <input type="text"
                                    class="form-control border-0 mt-0"
                                    pattern="\d*"
                                    maxlength="20"
                                    v-model="contacto.numero"/>
                                </div>

                                <div class="p-1 border mx-2 my-1">
                                    <p class="fw-light border-bottom mb-0">Correo Electrónico</p>
                                    <input type="text"
                                    placeholder="ejemplo@gmail.com"
                                    class="form-control border-0 mt-0 formato-inputs"
                                    maxlength="40"
                                    v-model="contacto.correo"/>
                                </div>
                            </div>
                            <div class="d-flex flex-wrap justify-content-around">

                                <button class="boton_cancelar px-5 py-1 border my-1" v-on:click="cancelarBoton">
                                    <h5>Cancelar</h5>
                                </button>

                                <button class="boton_cancelar px-5 py-1 border my-1" v-on:click="eliminarUsuario">
                                    <h5>Eliminar</h5>
                                    <!-- <i class="fa-solid fa-eraser"></i> -->
                                </button>

                                <button class="boton px-5 py-1 border my-1" v-on:click="submitForm">
                                    <h5>Guardar</h5>
                                </button>

                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>
import { useStore } from 'vuex';
import firebase from 'firebase';
import { auto } from '@popperjs/core';

export default{
    beforeMount(){
        if(this.store.state.isAuthenticated && this.store.state.user.rol === "admin"){
            this.$swal({
                allowEscapeKey: false,
                allowOutsideClick: false,
                width: auto,
                didOpen: () => {
                    this.$swal.showLoading();
                }
            })
            this.isAdmin = true;
            try{
                firebase
                    .firestore()
                    .collection("nomina")
                    .doc(this.$route.params.id)
                    .get()
                    .then((result) => {
                        this.empleado = result.data().usuario;
                    })
                firebase
                    .firestore()
                    .collection("contacto")
                    .doc(this.$route.params.id)
                    .get()
                    .then((result) => {
                        this.contacto = result.data().contacto;
                    })
                const interval = setInterval(() => {
                    if(this.empleado !== null){
                        if(this.empleado.photoName !== null){
                            firebase
                                .storage()
                                .ref()
                                .child(this.empleado.photoName)
                                .getDownloadURL()
                                .then(url => {
                                    this.photoURL = url
                                    this.$swal.close()
                                    console.log(url)
                                    this.listo = true;
                                    clearInterval(interval);
                                })
                        }
                        else{
                            this.$swal.close()
                            this.listo = true;
                            clearInterval(interval);
                        }
                    }
                }, 100);
            }catch(error){
                this.$swal({
                    icon: 'error',
                    text: error.message
                })
            }
        } else {
            this.$swal({
                icon: 'error',
                title: 'Tenemos un problema',
                text: 'Ha ocurrido un problema, lo sentimos',
                confirmButtonText: 'Volver'
            }).then(() => {
                this.$router.push("/")
            })
        }
    },
    setup(){
        const store = useStore()

        return{
            store
        }
    },
    data(){
        return{
            isAdmin: false,
            photoURL: null,
            empleado: null,
            contacto: null,
            listo: false,
            errors: "",
            pantallaGrande: ((window.innerWidth<1000) ? false : true),
            previewImage: null,
            image: null,
        }
    },
    methods: {
        onResize(){
            this.pantallaGrande = ((window.innerWidth<1000) ? false : true)
        },
        selectImage(){
            this.$refs.fileInput.click()
        },
        pickFile (){
            let input = this.$refs.fileInput
            let file = input.files
            this.image = file[0]
            if(file && file[0]){
                let reader = new FileReader
                reader.onload = e => {
                    this.previewImage = e.target.result
                }

                reader.readAsDataURL(file[0])
                this.$emit('input', file[0])
            }
        },
        cancelarBoton(){
            this.$router.go(-1)
        },
        submitForm: async function(){
            this.errors = "";
            
            if(!this.isNumber(this.empleado.NoIdentificacion) || !this.isNumber(this.empleado.celular) || !this.isCorreo(this.empleado.correo) || !this.isNumber(this.contacto.numero) || !this.isCorreo(this.contacto.correo)){
                this.errors = "Encontramos formato invalidos en el formulario "
                if(!this.isNumber(this.empleado.NoIdentificacion)){
                    this.errors += "(Número de identificación del empleado) "
                }
                if(!this.isNumber(this.empleado.celular)){
                    this.errors += "(Número telefónico del empleado) "
                }
                if(!this.isCorreo(this.empleado.correo)){
                    this.errors += "(Correo del empleado) "
                }
                if(!this.isNumber(this.contacto.numero)){
                    this.errors += "(Número telefónico del contacto) "
                }
                if(!this.isCorreo(this.contacto.correo)){
                    this.errors += "(Correo del contacto) "
                }
            }
            if(this.empleado.nombres === "" || this.empleado.apellidos === "" || this.empleado.fechaContracion === null ||
            this.empleado.tipoIdentificacion === "" || this.empleado.NoIdentificacion === "" || this.empleado.fechaNacimiento === null ||
            this.empleado.LugarNacimiento === "" || this.empleado.direccion === "" || this.empleado.celular === "" ||
            this.empleado.correo === "" || this.contacto.nombres === "" || this.contacto.apellidos === "" ||
            this.contacto.direccion === "" || this.contacto.numero === "" || this.contacto.correo === ""){
                this.errors = "Revisa el formulario, no debe haber campos vacios"
            }
            if(this.errors !== ""){
                this.$swal({
                    icon: 'error',
                    title: 'Problemas en el formulario',
                    text: this.errors
                });
            }
            else if(this.errors === ""){
                this.$swal({
                    icon: 'question',
                    title: 'Actualizar Usuario?',
                    text: 'Es la información que ingresaste correcta?',
                    html: `
                    <div class="d-flex border flex-column bd-highlight mb-3">
                    <div class="p-2 bd-highlight border">
                        <div class="d-flex justify-content-center p-0">
                        <h5 class="mb-3">`+this.empleado.nombres+` `+this.empleado.apellidos+`</h5>
                        </div>

                        <div class="d-flex justify-content-around mb-2 p-0">
                            <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Fecha de Ingreso</p>
                            <p class="my-1">`+this.empleado.fechaContracion+`</p>
                            </div>
                            <div class="m-0">
                            <p class="border-bottom fst-italic m-0 text-uppercase">`+this.empleado.tipoIdentificacion+`</p>
                            <p class="my-1">`+this.empleado.NoIdentificacion+`</p>
                            </div>
                        </div>

                        <div class="d-flex justify-content-around mb-2 p-0">
                            <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Nacimiento</p>
                            <p class="my-1">`+this.empleado.fechaNacimiento+`</p>
                            </div>
                            <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Ciudad</p>
                            <p class="my-1">`+this.empleado.LugarNacimiento+`</p>
                            </div>
                        </div>

                        <div class="d-flex justify-content-around mb-2 p-0">
                            <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Dirección</p>
                            <p class="my-1">`+this.empleado.direccion+`</p>
                            </div>
                            <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Número</p>
                            <p class="my-1">`+this.empleado.celular+`</p>
                            </div>
                        </div>

                        <div class="d-flex justify-content-around mb-2 p-0">
                            <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Correo</p>
                            <p class="my-1">`+this.empleado.correo+`</p>
                            </div>
                        </div>

                    </div>
                    <div class="p-2 bd-highlight border">

                        <div class="d-flex justify-content-center p-0">
                        <h5 class="mb-3">`+this.contacto.nombres+` `+this.contacto.apellidos+`</h5>
                        </div>

                        <div class="d-flex justify-content-around mb-2 p-0">
                        <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Dirección</p>
                            <p class="my-1">`+this.contacto.direccion+`</p>
                        </div>
                        <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Número</p>
                            <p class="my-1">`+this.contacto.numero+`</p>
                        </div>
                        </div>

                        <div class="d-flex justify-content-around mb-2 p-0">
                        <div class="m-0">
                            <p class="border-bottom fst-italic m-0">Correo</p>
                            <p class="my-1">`+this.contacto.correo+`</p>
                        </div>
                        </div>

                    </div>
                    </div>
                    `,
                    showCancelButton: true,
                    confirmButtonText: 'Actualizar',
                    cancelButtonText: 'Cancelar',
                    reverseButtons: true
                }).then((result) => {
                    this.$swal({
                        allowEscapeKey: false,
                        allowOutsideClick: false,
                        width: auto,
                        didOpen: () => {
                            this.$swal.showLoading();
                        }
                    })
                    if(result.isConfirmed){
                        if(this.previewImage){
                            const name_file = this.empleado.uid+"."+this.image.name.split(".")[1]
                            this.empleado.photoName = name_file
                            this.subirFoto(this.image, name_file)
                        }
                        this.actUsuario(this.empleado)
                        this.actContacto(this.contacto)                   
                    }
                })
            }
        },
        isNumber(aux){
            var numbs = '0123456789'
            for (var i in aux){
                if(!numbs.includes(aux[i])){
                    return false;
                }
            }
            return true;
        },
        isCorreo(aux){
            var i = aux.split("@")[1];
            if(i === undefined){
                return false;
            }
            if(!(i.split(".")[0] === "gmail" || i.split(".")[0] === "yahoo" || i.split(".")[0] === "hotmail")){
                return false;
            }
            if(!(i.split(".")[1] === "com" || i.split(".")[1] === "co" || i.split(".")[1] === "es")){
                return false;
            }
            return true;
        },
        async subirFoto(image, name_file){
            await firebase
                .storage()
                .ref()
                .child(name_file)
                .put(image)
                .then((snapshot) => {
                    console.log("imagen actualizada")
                })
        },
        async actUsuario(usuario){
            await firebase
                .firestore()
                .collection("nomina")
                .doc(this.empleado.uid)
                .set({usuario})
                .then(() => {
                    console.log("empleado actualizado")
                })
        },
        async actContacto(contacto){
            await firebase
                .firestore()
                .collection("contacto")
                .doc(this.empleado.uid)
                .set({contacto})
                .then(() => {
                    console.log("contacto actualizado")
                    this.$swal.close()
                    this.$router.back()
                })
        },
        async eliminarUsuario(){
            console.log("seeeadasdasd")
        }
    },
    mounted(){
        this.$nextTick(() => {
            window.addEventListener('resize',this.onResize);
        })
    },
    beforeDestroy(){
        window.removeEventListener('resize',this.onResize)
    },
}

</script>

<style>
  .imagePreviewWrapper {
    border-radius: 5%;
    background-size: 150px;
    background-position: 50%;
    width: 150px;
    height: 150px;
    display: block;
    margin-left: 10%;
    margin-top: 5%;
    cursor: pointer;
    font-size: 16px;
    background-repeat: no-repeat;
  }
  .caja{
    height: 20%;
    width: 250px;
  }
  .formato-inputs{
    text-align:center;
  }
  .boton_cancelar{
    border-radius: 250px;
    background: rgb(2,0,36);
    background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(246,197,197,1) 0%, rgba(228,60,60,1) 92%); 
  }
  .boton{
    border-radius: 250px;
    background: rgb(2,0,36);
    background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(188,200,189,1) 0%, rgba(58,221,66,1) 100%);
  }
  .editar_pp{
    margin-top: 95px;
  }
</style>