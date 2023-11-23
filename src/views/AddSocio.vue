<template>
    <div>
        <div class="titulo">
            <h1>Adicionar Sócio</h1>
        </div> 
        <form @submit.prevent="adicionarSocio">
            <section>
                <label for="">Nome</label>
                <input type="text" v-model="novoSocio.nome" id="nome">
            </section>

            <section>
                <label for="">Plano</label>
                <select v-model="novoSocio.plano">
                    <option value="Ouro">Ouro</option>
                    <option value="Prata">Prata</option>
                    <option value="Bronze">Bronze</option>
                </select>
            </section>

            <section>
                <label for="">Telefone</label>
                <input type="text" v-model="novoSocio.telefone" id="telefone">
            </section>

            <section>
                <label for="">Email</label>
                <input type="text" v-model="novoSocio.email" id="email">
            </section>

            <section>
                <label for="">Status</label>
                <select v-model="novoSocio.status">
                    <option value="ativo">Ativo</option>
                    <option value="desativo">Desativo</option>
                </select>
            </section>

            <section>
                <button class="botao botao-successo" type="submit">Adicionar Socio</button>
            </section>
        </form>
    </div> 
</template>

<script>


    export default {
        name: 'AddSocio',
        data(){
            return{
                novoSocio: {
                    nome: '',
                    plano: 'Ouro',
                    telefone: '',
                    email: '',
                    status: 'ativo'
                }
            }
        },
        methods:{
            adicionarSocio(){
                fetch(
                    'http://localhost:3000/socios/', {
                        method: 'POST',
                        headers: {"Content-Type": "application/json"},
                        body: JSON.stringify(this.novoSocio)
                    }
                ).then(
                    response =>{
                        if(!response.ok){
                            console.log("Deu ruim! Falha na requisição")
                        }
                        return response.json();
                    }
                ).then(
                    () => {
                        alert("Socio adicionado com sucesso");
                        this.novoSocio = { nome:'', plano: 'Ouro', telefone:'', email: '', status:'ativo'};
                    }
                ).catch(
                    error => {
                        console.log('Erro ao adicionar', error);
                    }
                );
            }
        }
    }
</script>

<style scoped>
form{
    display: flex;
    flex-direction: column;
    gap: 16px;
}
form > section{
    display: flex;
    flex-direction: column;
}
form label{
    color: white;
}

</style>