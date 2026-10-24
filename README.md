# Holiday Bridge 🌉

**Más días libres, menos días gastados.**

Holiday Bridge es una aplicación web para que cualquier persona que trabaje en España planifique sus vacaciones de 2027. Combina tus días de vacaciones con los festivos y los fines de semana para conseguir los periodos libres más largos gastando el menor número de días.

## Qué hace

- Muestra el calendario anual de 2027 con los festivos nacionales, autonómicos (incluidos los trasladados a lunes) y locales de tu municipio. Distingue con colores los fines de semana, los festivos y las vacaciones.
- Lleva la cuenta de tus días disponibles, asignados y pendientes. Solo descuentan los días laborables, de lunes a viernes y que no sean festivos.
- Sugiere periodos optimizados:
  - prioriza la eficiencia (días libres por cada día gastado) y la duración;
  - reparte el descanso a lo largo del año;
  - recomienda siempre en primer lugar la semana del 15 de agosto.
- Cada sugerencia indica las fechas, los días que gasta y los días libres seguidos que consigue. Se añade al calendario con un clic, y las sugerencias se recalculan con los días que te quedan.
- Puedes marcar o desmarcar días sueltos en el calendario, quitar un periodo completo para recuperar sus días o restablecer toda la planificación.
- Puedes añadir, quitar o corregir festivos a mano, por ejemplo si tu municipio no está en la lista o hay algún error.
- Exporta tus vacaciones a un archivo iCal (`.ics`) compatible con Outlook y Google Calendar. Cada periodo continuo se exporta como un único evento de día completo.
- Guarda todo en tu navegador (`localStorage`), sin cuentas ni registros.

## Cómo usarla

1. Abre `index.html` en el navegador. No hace falta instalar nada ni compilar.
2. Elige tu comunidad autónoma y tu municipio. Si tu municipio no aparece, elige «Otro municipio» y añade tus festivos locales.
3. Ajusta tus días de vacaciones. Por defecto son 24, y puedes sumar los que te queden del año anterior.
4. Acepta sugerencias o haz clic en los días laborables del calendario.
5. Descarga el `.ics` e impórtalo en tu calendario.

### Publicarla en GitHub Pages

En el repositorio, ve a *Settings → Pages*, elige la rama y la carpeta raíz (`/`) y guarda. La aplicación se publicará tal cual.

## Datos de festivos

Los festivos están en la constante `DATOS_FESTIVOS`, al principio del `<script>` de `index.html`, separados del resto de la lógica y organizados por año:

```js
const DATOS_FESTIVOS = {
  2027: {
    nacional:    { estado, fuente, festivos: [['2027-01-01', 'Año Nuevo'], …] },
    comunidades: {
      MD: { nombre, estado, fuente, festivos: […],
            municipios: { madrid: { nombre, estado, fuente, festivos: […] } } }
    }
  }
};
```

Cada festivo se escribe como `[fecha, nombre, estado?, ámbito?]`:

- **`oficial`**: la fecha figura en una norma o acuerdo publicado (BOE, boletín autonómico, BOP o acuerdo del pleno municipal).
- **`provisional`**: es una fecha habitual o la han publicado medios o terceros, así que conviene revisarla. En el calendario aparece con el borde discontinuo.

Fuentes principales para 2027:

- Calendario estatal: Resolución de 8 de octubre de 2026 de la Dirección General de Trabajo, publicada en el BOE del 13 de octubre de 2026 (BOE-A-2026-21254).
- Normas autonómicas: decretos de cada comunidad. La fuente concreta figura en los datos y en la propia aplicación.

Los datos se recopilaron en octubre de 2026. Muchos festivos locales aún no estaban publicados en los boletines, por lo que figuran como provisionales.

### Cómo actualizar los festivos

- **Corregir un dato:** edita la fecha o el nombre en `DATOS_FESTIVOS` y cambia su estado a `'oficial'` cuando lo confirmes en el boletín.
- **Añadir un municipio:** añade una entrada dentro de `municipios` de su comunidad, con un identificador sin espacios.
- **Añadir otro año (por ejemplo, 2028):** crea la clave `2028` con la misma estructura y cambia `ANIO_ACTIVO` en la sección «Configuración general». La planificación de cada año se guarda aparte en el navegador si cambias también `CLAVE_STORAGE`.

## Apariencia

Los colores, la tipografía y los espaciados están definidos como variables CSS en `:root`, al principio del `<style>`. Puedes cambiar el aspecto sin tocar el resto del código.
