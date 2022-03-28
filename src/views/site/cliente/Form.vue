<template>
  <div class="container">
    <card shadow type="secondary">
      <div slot="header" class="bg-white border-0">
        <div class="row align-items-center">
          <div class="col-8">
            <h3 v-if="$route.name === 'cliente.auto_editar'" class="mb-0">Editar Meus Dados</h3>
            <h3 v-else class="mb-0">Novo Cliente</h3>
          </div>
          <div class="col-4 text-right">
            <b-btn variant="primary" @click="onSubmit">Salvar</b-btn>
          </div>
        </div>
      </div>
      <template>
        <form @submit="onSubmit">
          <h6 class="heading-small text-muted mb-4">Meus Dados</h6>
          <div class="pl-lg-4">
            <div class="row">
              <div class="col-lg-4">
                <base-input alternative=""
                            label="Nome *"
                            placeholder="Nome"
                            input-classes="form-control-alternative"
                            v-model="model.nome"
                            required
                />
              </div>
              <div class="col-lg-4">
                <base-input alternative=""
                            label="CPF *"
                            placeholder="000.000.000-00"
                            input-classes="form-control-alternative"
                            v-model="model.CPF"
                            v-mask="'###.###.###-##'"
                            :valid="isCPFValid"
                            :disabled="this.$route.name === 'cliente.auto_editar' && isCPFValid"
                            required
                />
              </div>
              <div class="col-lg-4">
                <b-form-group label="Sexo *" label-class="form-control-label">
                  <b-select v-model="model.sexo" :options="['Masculino', 'Feminino']" required/>
                </b-form-group>
              </div>
            </div>
            <div class="row">
              <div class="col-lg-6">
                <base-input alternative=""
                            label="Telefone *"
                            placeholder="Telefone"
                            input-classes="form-control-alternative"
                            v-model="model.phone"
                            v-mask="['(##) ####-####', '(##) #####-####']"
                            :valid="isPhoneValid"
                />
              </div>
              <div class="col-lg-6">
                <base-input alternative=""
                            label="Data de Nascimento *"
                            placeholder="Nascimento"
                            input-classes="form-control-alternative"
                            type="date"
                            v-model="model.nascimento"
                />
              </div>
            </div>
            <div class="row">
              <div class="col-lg-6">
                <base-input alternative=""
                            label="Email *"
                            placeholder="nome@email.com"
                            input-classes="form-control-alternative"
                            v-model="model.email"
                            :disabled="this.$route.name === 'cliente.auto_editar'"
                            required
                />
              </div>
              <div class="col-lg-6">
                <base-input alternative=""
                            label="Senha *"
                            type="password"
                            placeholder=" + + + +"
                            input-classes="form-control-alternative"
                            v-model="model.password"
                            required
                />
              </div>
            </div>
          </div>
          <hr class="my-4"/>
        </form>
      </template>
    </card>
  </div>
</template>

<script>
  import { mapActions, mapGetters } from 'vuex'
  import ClienteRepository from '@/repositories/Cliente'
  import { mask } from 'vue-the-mask'

  export default {
    name: 'Form',
    directives: { mask },
    computed: {
      ...mapGetters({
        cliente: 'cliente/current'
      }),
      isCPFValid() {
        let Soma;
        let Resto;
        Soma = 0;
        let strCPF = this.model.CPF.replace(/\D/g, '')
        if (strCPF.length < 11)
          return null

        if (
          strCPF === "00000000000" ||
          strCPF === "11111111111" ||
          strCPF === "22222222222" ||
          strCPF === "33333333333" ||
          strCPF === "44444444444" ||
          strCPF === "55555555555" ||
          strCPF === "66666666666" ||
          strCPF === "77777777777" ||
          strCPF === "88888888888" ||
          strCPF === "99999999999"
        ){
          return false;
        }

        for (let i=1; i<=9; i++)
          Soma = Soma + parseInt(strCPF.substring(i-1, i)) * (11 - i);
        Resto = (Soma * 10) % 11;
        if ((Resto === 10) || (Resto === 11))
          Resto = 0;
        if (Resto !== parseInt(strCPF.substring(9, 10)) )
          return false;
        Soma = 0;
        for (let i = 1; i <= 10; i++)
          Soma = Soma + parseInt(strCPF.substring(i-1, i)) * (12 - i);
        Resto = (Soma * 10) % 11;
        if ((Resto === 10) || (Resto === 11))
          Resto = 0;
        if (Resto !== parseInt(strCPF.substring(10, 11) ) )
          return false;
        return true;
      },
      isPhoneValid(){
        //retira todos os caracteres menos os numeros
        let telefone = this.model.phone.replace(/\D/g, '')
        if (telefone.length < 10)
          return null
        
        //verifica se tem a qtde de numero correto
        if(!(telefone.length >= 10 && telefone.length <= 11)) return false;
        
        //Se tiver 11 caracteres, verificar se começa com 9 o celular
        if (telefone.length == 11 && parseInt(telefone.substring(2, 3)) != 9) return false;
          
        //verifica se não é nenhum numero digitado errado (propositalmente)
        for(let n = 0; n < 10; n++){
          //um for de 0 a 9.
          //estou utilizando o metodo Array(q+1).join(n) onde "q" é a quantidade e n é o 	  
          //caractere a ser repetido
          if(telefone == new Array(11).join(n) || telefone == new Array(12).join(n)) return false;
          }
          //DDDs validos
          let codigosDDD = [
            11, 12, 13, 14, 15, 16, 17, 18, 19,
            21, 22, 24, 27, 28, 31, 32, 33, 34,
            35, 37, 38, 41, 42, 43, 44, 45, 46,
            47, 48, 49, 51, 53, 54, 55, 61, 62,
            64, 63, 65, 66, 67, 68, 69, 71, 73,
            74, 75, 77, 79, 81, 82, 83, 84, 85,
            86, 87, 88, 89, 91, 92, 93, 94, 95,
            96, 97, 98, 99
          ];
          //verifica se o DDD é valido (sim, da pra verificar rsrsrs)
          if(codigosDDD.indexOf(parseInt(telefone.substring(0, 2))) == -1) return false;
          
          //  E por ultimo verificar se o numero é realmente válido. Até 2016 um celular pode 
          //ter 8 caracteres, após isso somente numeros de telefone e radios (ex. Nextel)
          //vão poder ter numeros de 8 digitos (fora o DDD), então esta função ficará inativa
          //até o fim de 2016, e se a ANATEL realmente cumprir o combinado, os numeros serão
          //validados corretamente após esse período.
          //NÃO ADICIONEI A VALIDAÇÂO DE QUAIS ESTADOS TEM NONO DIGITO, PQ DEPOIS DE 2016 ISSO NÃO FARÁ DIFERENÇA
          //Não se preocupe, o código irá ativar e desativar esta opção automaticamente.
          //Caso queira, em 2017, é só tirar o if.
          //if(new Date().getFullYear() < 2017) return true;
          if (telefone.length == 10 && [2, 3, 4, 5, 7].indexOf(parseInt(telefone.substring(2, 3))) == -1) return false;

          //se passar por todas as validações acima, então está tudo certo
          return true;
        
      }
    },
    data () {
      return {
        model: {
          nome: '',
          CPF: '',
          phone: '',
          email: '',
          password: '',
          nascimento: '',
          sexo: '',
        }
      }
    },
    methods: {
      ...mapActions([
        'cliente/listMe'
      ]),
      validaRetornoErro (error) {
        const data = error.response ? error.response.data : null
        if (data.errors && data.message === 'The given data was invalid.') {
          // const reverse = data.errors.reverse()
          Object.keys(data.errors).map(campo => {
            data.errors[campo].map(msg => {
              this.$notify({
                type: 'danger',
                title: msg,
                verticalAlign: 'top',
                horizontalAlign: 'center'
              })
            })
          })
        }
      },
      async onSubmit (evt) {
        evt.preventDefault()
        if ( typeof this.isCPFValid === "boolean" && !this.isCPFValid){
          this.$notify({
            type: 'danger',
            title: 'CPF Inválido',
            verticalAlign: 'bottom',
            horizontalAlign: 'center'
          })
          return
        }
        if ( typeof this.isPhoneValid === "boolean" && !this.isPhoneValid){
          this.$notify({
            type: 'danger',
            title: 'Telefone Inválido',
            verticalAlign: 'bottom',
            horizontalAlign: 'center'
          })
          return
        }
        if (this.$route.name === 'cliente.auto_editar') {
          this.update()
        } else {
          this.create()
        }
      },
      create () {
        ClienteRepository.post(this.model).then(() => {
          this.$notify({
            type: 'success',
            title: `Dados Salvos com Sucesso!`,
            verticalAlign: 'bottom',
            horizontalAlign: 'center'
          })
          this.$router.push({ name: 'cliente' })
        }).catch(error => {
          this.validaRetornoErro(error)
        })
      },
      update () {
        ClienteRepository.put(this.cliente.id, this.model).then(() => {
          this.$notify({
            type: 'success',
            title: `Dados Atualizados com Sucesso!`,
            verticalAlign: 'bottom',
            horizontalAlign: 'center'
          })
          this.$router.push({ name: 'cliente' })
        }).catch(error => {
          this.validaRetornoErro(error)
        })
      }
    },
    async mounted () {
      if (this.$route.name === 'cliente.auto_editar') {
        await this['cliente/listMe'](this.$route.params.id)
        this.model = {
          ...this.model,
          ...this.cliente
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
</style>
