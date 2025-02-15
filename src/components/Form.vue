<script setup>
import { reactive } from 'vue';

const estado = reactive({
    filtro: 'selecionar',

    primeiroNumero: 0,
    segundoNumero: 0,
})

const resultado = () => {
    const { filtro, primeiroNumero, segundoNumero } = estado;

    if (Number.isNaN(primeiroNumero) || Number.isNaN(segundoNumero)) {
        return 'Por favor, preencha ambos os números';
    }

    switch (filtro) {
        case 'somar':
            return primeiroNumero + segundoNumero
        case 'subtrair':
            return primeiroNumero - segundoNumero
        case 'dividir':
            return segundoNumero !== 0 ? primeiroNumero / segundoNumero : 'Escolha um número diferente de 0'
        case 'multiplicar':
            return primeiroNumero * segundoNumero
        default:
            return 'Selecione um operador'
    }
}
</script>

<template>
    <main class="container border border-dark p-5" style="height: 250px;">
        <form class="d-flex justify-content-around">
            <input required @change="e => estado.primeiroNumero = parseFloat(e.target.value)"
                class="text-center px-150 w-25" type="number" placeholder="digite o primeiro número" />
            <input required @change="e => estado.segundoNumero = parseFloat(e.target.value)"
                class="text-center px-150 w-25" type="number" placeholder="digite o segundo número" />
            <select @change="e => estado.filtro = e.target.value" class="form-control w-25">
                <option value="selecionar">Selecione a operação desejada</option>
                <option value="somar">Somar</option>
                <option value="subtrair">Subtrair</option>
                <option value="dividir">Dividir</option>
                <option value="multiplicar">Multiplicar</option>
            </select>
        </form>
        <p>Operação selecionada: {{ estado.filtro }}</p>
        <p>Resultado: {{ resultado() }}</p>
    </main>
</template>