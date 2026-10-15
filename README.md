# Control Concreto – iPhone (Codemagic + TestFlight)

App de iPhone del control de llegadas de concreto. Es la versión web (carpeta `www/`) empaquetada
como app nativa con Capacitor. Funciona sin internet; datos y fotos quedan dentro del iPhone.
La carpeta `ios/` no se sube: Codemagic la crea en cada compilación.

## Requisitos (una sola vez)
1. Cuenta de **Apple Developer Program** (pago anual), de la empresa o personal.
2. developer.apple.com > Certificates, IDs & Profiles > Identifiers: registrar el Bundle ID
   `co.obra.controlconcreto` (App IDs > App).
3. App Store Connect > Apps > "+" > Nueva app: iOS, nombre "Control Concreto", ese Bundle ID.
   Anotar el **Apple ID** numérico que aparece en App Information.
4. App Store Connect > Users and Access > Integrations > App Store Connect API: crear una llave
   con acceso **App Manager** y descargar el archivo .p8 (solo se puede descargar una vez).
5. Codemagic > Team settings > Integrations > Developer Portal > Connect: nombre **CodemagicASC**,
   con el Issuer ID, el Key ID y el archivo .p8.
6. Codemagic > Team settings > Code signing identities:
   - iOS certificates > Generate certificate > tipo Apple Distribution.
   - iOS provisioning profiles > Fetch profiles > tipo App Store, Bundle ID `co.obra.controlconcreto`.
7. En `codemagic.yaml`, reemplazar `APP_STORE_APPLE_ID: 0000000000` por el Apple ID del paso 3.

## Compilar
Codemagic > Add application > conectar este repositorio de GitHub > "Ionic Capacitor App"
> Start new build > workflow **iOS - TestFlight**. Tarda unos 15 minutos.
Al terminar, la compilación aparece en TestFlight en 10 a 30 minutos más.

## Probar en el iPhone
1. Instalar **TestFlight** desde la App Store.
2. App Store Connect > la app > TestFlight > Internal Testing > agregar tu cuenta como probador.
3. Abrir la invitación en el iPhone e instalar.

## Actualizar
Cambia los archivos de `www/` y vuelve a compilar en Codemagic. El número de compilación sube solo.
