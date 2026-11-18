# Caffè al bar – dataviz Radar QN

| Dataviz | URL | Dati |
|---|---|---|
| Quanto hai pagato il caffè? (calcolatore, andamento dal 2021, beeswarm) | https://cosimofire.github.io/caffe/caffe/ | `data/caffe-province.csv`, `data/caffe-serie.csv` |

**Fonte:** Osservatorio prezzi del ministero delle Imprese e del Made in Italy, voce "Caffè espresso al bar (1 pz)".

**Dati:** `data/caffe-serie.csv` contiene la serie mensile del prezzo medio per provincia da gennaio 2021 (usata dal grafico a linea, che mostra la provincia scelta). `data/caffe-province.csv` contiene, per ognuna delle 64 province rilevate, l'ultimo mese disponibile con prezzo minimo, massimo e medio (separatore `;`, virgola decimale). Il mese di riferimento della pagina è il più recente presente nel file; le province con un dato più vecchio sono segnate come "dato non aggiornato" (punto vuoto). Per aggiornare la dataviz basta sostituire il CSV.

## Sfondo e logo

Con la skill radar-dataviz V02_1 la pagina riconosce da sola i quattro sfondi QN (grigio, bianco, nero, notte) e sceglie il tema di conseguenza; il logo QN compare in alto a destra. Per le anteprime senza CMS: `?bg=grigio`, `?bg=bianco`, `?bg=nero`, `?bg=notte`.

## Snippet per il CMS

Iframe seguito dallo script che adatta l'altezza e passa il tema del sito. Se nell'articolo ci sono più dataviz, lo script può restare in ognuna (grazie al controllo `__radarQNv2` non lavora due volte) oppure si tiene una volta sola.

```html
<iframe src="https://cosimofire.github.io/caffe/caffe/" width="100%" height="1080" frameborder="0" scrolling="no" title="Quanto hai pagato il caffè?"></iframe>
<script>
(function(){if(window.__radarQNv2)return;window.__radarQNv2=1;var O="https://cosimofire.github.io";var MQ=window.matchMedia("(prefers-color-scheme:dark)");function frames(){return Array.prototype.filter.call(document.getElementsByTagName("iframe"),function(f){return(f.getAttribute("src")||"").indexOf(O+"/")===0;});}function theme(){var t=document.documentElement.getAttribute("data-theme");return t==="dark"||t==="light"?t:(MQ.matches?"dark":"light");}function bgOf(el){for(;el&&el.nodeType===1;el=el.parentElement){var c=getComputedStyle(el).backgroundColor;if(c&&c !=="transparent"&&!/rgba\([^)]*,\s*0\)$/.test(c))return c;}return null;}function send(f){try{f.contentWindow.postMessage({sentinel:"radar-qn",type:"theme",theme:theme(),bg:bgOf(f.parentElement)},O);}catch(e){}}function sendAll(){frames().forEach(send);}window.addEventListener("message",function(e){if(e.origin !==O)return;var d=e.data;if(!d||d.sentinel !=="radar-qn"||d.type !=="height")return;frames().forEach(function(f){if(f.contentWindow !==e.source)return;var h=Math.ceil(+d.height);if(h > 0&&20000 > h)f.style.height=h+"px";send(f);});});new MutationObserver(function(){sendAll();setTimeout(sendAll,400);}).observe(document.documentElement,{attributes:true,attributeFilter:["data-theme"]});if(MQ.addEventListener)MQ.addEventListener("change",sendAll);})();
</script>
```
