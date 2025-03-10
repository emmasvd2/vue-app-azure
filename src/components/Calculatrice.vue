<script setup>
import { ref } from 'vue';
import EcranCal from './EcranCal.vue';
import BoutonCal from './BoutonCal.vue';

const leftOperator = ref("");
const rightOperator = ref("");
const operation = ref("");
const result = ref("");

const handleClick = (value) => {
    if (!isNaN(value)) { // Si c'est un chiffre
        if (operation.value === "") {
            leftOperator.value += value;
        } else {
            rightOperator.value += value;
        }
    } else if (value === "C") { // Réinitialisation
        leftOperator.value = "";
        rightOperator.value = "";
        operation.value = "";
        result.value = "";
    } else if (value === "=") { // Calculer le résultat
        if (leftOperator.value && rightOperator.value && operation.value) {
            const left = parseFloat(leftOperator.value);
            const right = parseFloat(rightOperator.value);
            
            switch (operation.value) {
                case "+":
                    result.value = left + right;
                    break;
                case "-":
                    result.value = left - right;
                    break;
                case "*":
                    result.value = left * right;
                    break;
                case "/":
                    result.value = right !== 0 ? left / right : "Erreur";
                    break;
            }

            leftOperator.value = result.value.toString();
            rightOperator.value = "";
            operation.value = "";
        }
    } else { // Si c'est un opérateur
        if (leftOperator.value !== "" && rightOperator.value === "") {
            operation.value = value;
        }
    }
};
</script>

<template>
    <div class="border">
        <EcranCal :operation="operation" :leftOperator="leftOperator" :rightOperator="rightOperator" :result="result"/>
        
        <div class="button">
            <div class="ligne">
                <BoutonCal value="+" @send-value="handleClick"/>
                <BoutonCal value="-" @send-value="handleClick"/>
                <BoutonCal value="=" @send-value="handleClick"/>
            </div>
            <div class="ligne">
                <BoutonCal value="/" @send-value="handleClick"/>
                <BoutonCal value="*" @send-value="handleClick"/>
                <BoutonCal value="C" @send-value="handleClick"/>
            </div>
            <div class="ligne">
                <BoutonCal value="9" @send-value="handleClick"/>
                <BoutonCal value="8" @send-value="handleClick"/>
                <BoutonCal value="7" @send-value="handleClick"/>
            </div>
            <div class="ligne">
                <BoutonCal value="6" @send-value="handleClick"/>
                <BoutonCal value="5" @send-value="handleClick"/>
                <BoutonCal value="4" @send-value="handleClick"/>
            </div>
            <div class="ligne">
                <BoutonCal value="3" @send-value="handleClick"/>
                <BoutonCal value="2" @send-value="handleClick"/>
                <BoutonCal value="1" @send-value="handleClick"/>
            </div>
            <div>
                <BoutonCal value="0" @send-value="handleClick"/>
            </div>
        </div>
    </div> 
</template>

<style scoped>
.border {
    display: flex;
    flex-direction: column;
    border: 2px solid white;
    padding: 5px;
    background-color: white;
}

.button {
    margin-top: 5px;
    display: flex;
    flex-direction: column;
    gap: 5px;
}

.ligne {
    display: flex;
    gap: 5px;
}
</style>
