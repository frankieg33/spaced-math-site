---
title: "Mate Diaria"
description: "Ejercicios de matemáticas con repetición espaciada para iPhone y iPad"
---

# Política de privacidad — Mate Diaria

**Fecha de entrada en vigor:** 2026-05-21
**Última actualización:** 2026-06-10

Esta política describe cómo la app de iOS Mate Diaria ("la App") trata tu información. Se aplica a partir de la v1.0, incluido el modelo de uso compartido por CloudKit de un solo hogar de la v3 (que sustituye al uso compartido por perfil de la v2.0).

## Resumen en lenguaje sencillo

- No tenemos servidores. No recopilamos ninguna información personal.
- Todo permanece en tu dispositivo a menos que actives la **sincronización de iCloud**, en cuyo caso Apple, no nosotros, lo guarda en tu cuenta privada de iCloud.
- La App usa tu micrófono solo mientras respondes a un problema en modo voz. El audio lo procesa el reconocimiento de voz de Apple (en el dispositivo, clase Siri) y se descarta de inmediato; nunca lo almacenamos, subimos ni analizamos.
- No hay rastreadores de terceros, ni anuncios, ni SDK de analítica.

## Qué guarda la App en tu dispositivo

- **Perfiles.** Nombre, emoji, color y ajustes por perfil.
- **Estado de repetición espaciada.** Para cada tarjeta (p. ej. `7 + 8`): fecha del próximo repaso, dificultad, estabilidad y número de repasos.
- **Actividad.** Un recuento diario de repasos completados por perfil (usado para la etiqueta de racha y la pantalla de Estadísticas).
- **Errores.** Una cola de problemas que has respondido mal hace poco para que la App pueda volver a mostrarlos.
- **Preferencias.** Interruptores de toda la App, como si la sincronización de iCloud está activada.

Todo esto se escribe en la carpeta de Documentos aislada de la propia App y en `UserDefaults`. La App no puede leer los datos de otras apps, y otras apps no pueden leer los datos de la App.

## Qué guarda opcionalmente la App en iCloud

La sincronización de iCloud está **desactivada de forma predeterminada**. Cuando la activas (icono del engranaje → **Ajustes → Sincronización → Usar iCloud**), la App escribe los mismos datos descritos arriba en tu iCloud privado mediante la API **CloudKit** de Apple. Es tu iCloud, accesible solo para ti en los dispositivos con sesión iniciada con el mismo ID de Apple. Nosotros no tenemos acceso.

- Los datos exactos que se sincronizan: perfiles, estados de tarjetas, actividad, errores y (opcionalmente) metadatos del uso compartido del hogar (un nombre que elijas para tu hogar).
- La sincronización de iCloud **no** incluye el contenido de ninguna grabación de voz ni ninguna analítica.
- Cuando inicias sesión con un ID de Apple distinto, la App detecta el cambio y desactiva la sincronización hasta que la vuelves a activar explícitamente, para que los datos no se suban en silencio a otra cuenta.
- Borrar un perfil desde **Gestionar perfiles** elimina el perfil del dispositivo y (cuando iCloud está disponible en el ID de Apple original) también de tu copia de iCloud.

## Uso compartido del hogar

En la v3, el uso compartido se produce a nivel de **hogar** en lugar de por perfil. Abre el icono del engranaje → **Ajustes → Hogar → Configurar hogar**, da nombre a tu hogar e invita a familiares mediante la hoja de uso compartido estándar de iOS (Mensajes, Mail o AirDrop).

- Todos los perfiles del dispositivo del propietario pertenecen al hogar. Invitar a un familiar los comparte todos a la vez.
- Los datos viven en el **iCloud del propietario del hogar**. Los participantes no guardan una copia aparte en su propio iCloud; su actividad de estudio se escribe directamente en el CloudKit del propietario mediante el modelo de permisos CKShare con alcance de zona de Apple.
- Unirse a un hogar es **destructivo en el dispositivo que se une**: los perfiles locales existentes del participante se sustituyen por los del hogar. Antes de unirse, la App ofrece una opción **Exportar perfiles a archivo** para que guardes una copia JSON de tus datos actuales y vuelvas a importarla más tarde si cambias de opinión.
- Si el propietario disuelve el hogar (Ajustes → Hogar → Disolver) o cierra sesión en iCloud, los participantes pierden el acceso en vivo en su próxima sincronización. La caché local de perfiles del hogar pasa a ser suya (sin borrado destructivo al salir).
- Un participante puede salir de un hogar en cualquier momento (Ajustes → Hogar → Salir). Al salir, conserva los perfiles del hogar en su dispositivo como propios.
- El límite de `CKShare` de Apple es de 100 participantes por elemento compartido. La escala natural de un hogar es de ~6.

## Exportar / Importar (copia de seguridad JSON)

En **Ajustes → Copia de seguridad** puedes:

- **Exportar perfiles a archivo**: guardar un archivo JSON con todos los perfiles del dispositivo actual (cualquier estado de hogar). Útil como copia de seguridad manual o antes de operaciones destructivas.
- **Importar perfiles desde archivo**: restaurar una exportación anterior. El modo **Combinar** añade los perfiles que falten y actualiza los existentes si la copia importada es más reciente. El modo **Reemplazar** borra los perfiles locales e instala el conjunto importado; solo está disponible cuando no estás en un hogar.

## Micrófono y reconocimiento de voz

Cuando el modo voz está activado, mientras respondes a un problema la App:

1. Captura audio del micrófono en directo con `AVAudioEngine`.
2. Lo transmite a `SFSpeechRecognizer` (el framework de Apple). En los dispositivos iOS modernos, el reconocimiento se ejecuta en el dispositivo de forma predeterminada; algunas configuraciones pueden usar los servidores de reconocimiento de voz de Apple.
3. Lee los dígitos transcritos y califica la respuesta.
4. Detiene la captura en cuanto se obtiene una respuesta final.

No conservamos audio, transcripciones ni ninguna señal derivada. No transmitimos audio a ninguna parte que no sea el `SFSpeechRecognizer` de Apple. La App solicita `NSMicrophoneUsageDescription` y `NSSpeechRecognitionUsageDescription` en el primer uso; si se deniega cualquiera de los permisos, el modo voz se desactiva automáticamente y se usa el teclado numérico en pantalla.

## Registros de diagnóstico

La App emite eventos de diagnóstico no estructurados mediante el framework estándar `OSLog` de Apple (p. ej. "sesión de estudio finalizada, correctas=12 incorrectas=3"). Estos registros:

- Permanecen en el dispositivo.
- Solo son visibles para ti, en Console.app mientras el dispositivo está conectado a un Mac.
- Usan la clasificación de privacidad `.private` de Apple para cualquier valor potencialmente identificable (id de perfil, nombre de perfil), de modo que esos valores se ocultan en las versiones publicadas.

No recopilamos, recuperamos ni transmitimos el contenido de `OSLog`.

## Datos que NO recopilamos

- Tu nombre, correo o datos de contacto.
- Tu ubicación.
- Cualquier identificador de dispositivo (IDFA, IDFV, id de publicidad).
- Informes de fallos más allá de lo que Apple pueda recopilar a través de tus ajustes de iOS.
- Cualquier analítica o telemetría de comportamiento.
- Información de pago o facturación (las compras las gestiona íntegramente Apple).

## Privacidad de los menores

Mate Diaria está diseñada para ser segura para los niños. Como la App no recopila información personal y no contacta con terceros, cumple la definición de "sin información personal" de COPPA. No mostramos anuncios y no hay cuentas ni funciones sociales. Mate Diaria incluye una única compra dentro de la app (un desbloqueo de la app completa); como la app está diseñada para niños, se muestra una verificación de adultos antes de cualquier compra, tal como exigen las normas de la categoría Niños de Apple. Todos los pagos y cualquier canje de códigos los gestiona Apple a través del App Store. La App nunca ve ni almacena tus datos de pago.

## Tus opciones

- **Desactivar el modo voz** en cualquier momento por perfil (Ajustes → Modo voz) o de forma global denegando el permiso del micrófono en los Ajustes de iOS.
- **Desactivar la sincronización de iCloud** en cualquier momento (icono del engranaje → Ajustes → Sincronización → Usar iCloud → desactivado). Desactivarla no borra las copias de iCloud; borra cada perfil individualmente si quieres eliminarlas.
- **Disolver o salir de un hogar** (Ajustes → Hogar → Disolver / Salir) para dejar de compartir. Disolver revoca el acceso de los participantes a tu hogar; salir conserva los perfiles del hogar en tu dispositivo como propios.
- **Exportar perfiles a un archivo** (Ajustes → Copia de seguridad → Exportar) y guardarlo localmente: una copia de seguridad manual que nunca toca iCloud.
- **Restablecer el progreso de un perfil** sin borrar el perfil (Ajustes del perfil → Restablecer).
- **Borrar un perfil** (Gestionar perfiles → desliza o toca para borrar): también elimina la copia de iCloud cuando la sincronización está activada. Repite por perfil para eliminarlo todo.

## Cambios en esta política

Si cambiamos esta política, la nueva versión estará disponible en la misma URL con una fecha de **Última actualización** actualizada. Los cambios importantes también se indicarán en las notas de la versión de la App.

## Contacto

¿Preguntas sobre esta política o tus datos? Correo **spacedmath@gmail.com**.
