<script lang="ts">
    enum Sexe {
        homme,
        femme
    };
    enum Activite {
        sedentaire,
        actif,
        sportif
    }

    let sexe: Sexe = Sexe.femme;
    let activite: Activite = Activite.sedentaire;
    let poids: number = 60;
    let taille: number = 170;
    let age: number = 40;
    let imc: number;
    let calories: number;
    let poidsIdeal: number;

    const inchToCm = function(valueInInch: number) {
        return valueInInch * 2.54;
    }
    const cmToInch = function(valueInCm: number) {
        return valueInCm / 2.54;
    }
    const poundToKg = function(valueInPound: number) {
        return valueInPound * 0.454;
    }

    $: {
        imc = poids / Math.pow(taille / 100, 2);
        calories = (sexe === Sexe.femme ? 0.963 : 1.083) * Math.pow(poids, 0.48) * Math.pow(taille, 0.5) * Math.pow(age, -0.13) * (1000 / 4.1855) * (activite === Activite.sedentaire ? 1.375 : (activite === Activite.actif ? 1.56 : 1.82));
        poidsIdeal = poundToKg(age > 18 ?
            (sexe === Sexe.femme ? -111.621 + (3.636 * (cmToInch(taille))) : -130.736 + (4.064 * cmToInch(taille))) :
            (sexe === Sexe.femme ? (-77.55796 + (6.93728 * cmToInch(taille)) - (0.171703 * Math.pow(cmToInch(taille), 2)) + (0.001726 * Math.pow(cmToInch(taille), 3))) : (-59.6035 + (5.2878 * cmToInch(taille)) - (0.123939 * Math.pow(cmToInch(taille), 2)) + (0.00128936 * Math.pow(cmToInch(taille), 3)))));
        //poidsIdeal = (3.636 * cmToInch(taille) -111.621) * 0.454;
    }
</script>

<div class="form-field">
    <span>Je suis</span>
    <label>
        <input bind:group={sexe} type="radio" value={Sexe.femme}/> une femme
    </label>
    <label>
        <input bind:group={sexe} type="radio" value={Sexe.homme}/> un homme
    </label>
</div>

<div class="form-field">
    <label>
        J'ai (en années) <input type="number" min=1 max=150 bind:value={age}/>
    </label>
</div>

<div class="form-field">
    <span>Je suis</span>
    <label>
        <input bind:group={activite} type="radio" value={Activite.sedentaire}/> sédentaire
    </label>
    <label>
        <input bind:group={activite} type="radio" value={Activite.actif}/> actif
    </label>
    <label>
        <input bind:group={activite} type="radio" value={Activite.sportif}/> sportif
    </label>
</div>

<div class="form-field">
    <label>
        Je mesure (en cm) <input type="number" min=1 max=250 bind:value={taille}/>
    </label>
</div>

<div class="form-field">
    <label>
        Je pèse (en kg) <input type="number" min=1 max=250 bind:value={poids}/>
    </label>
</div>
<br/>
<div>
    <span>Mon IMC est de {Intl.NumberFormat('fr-fr', {minimumFractionDigits: 0, maximumFractionDigits: 2}).format(imc)}</span>
</div>
<div>
    <span>Je dépense {Intl.NumberFormat('fr-fr', {minimumFractionDigits: 0, maximumFractionDigits: 0}).format(calories)} k calories par jour (formule de Black et al)</span>
</div>
<div>
    <span>Mon poids idéal est de {Intl.NumberFormat('fr-fr', {minimumFractionDigits: 0, maximumFractionDigits: 0}).format(poidsIdeal)} kg (formule de Pek)</span>
</div>