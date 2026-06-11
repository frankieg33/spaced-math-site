---
title: "Mate Diária"
description: "Exercícios de matemática com repetição espaçada para iPhone e iPad"
---

# Política de Privacidade — Mate Diária

**Data de vigência:** 2026-05-21
**Última atualização:** 2026-06-10

Esta política descreve como o app de iOS Mate Diária ("o App") trata suas informações. Aplica-se da v1.0 em diante, incluindo o modelo de compartilhamento por CloudKit de família única da v3 (que substitui o compartilhamento por perfil da v2.0).

## Resumo em linguagem simples

- Não operamos nenhum servidor. Não coletamos nenhuma informação pessoal.
- Tudo permanece no seu dispositivo, a menos que você ative a **sincronização do iCloud**, caso em que a Apple, não nós, a armazena na sua conta privada do iCloud.
- O App usa seu microfone apenas enquanto você responde a um problema no modo de voz. O áudio é processado pelo reconhecimento de fala da Apple (no dispositivo, classe Siri) e descartado imediatamente; nunca o armazenamos, enviamos ou analisamos.
- Não há rastreadores de terceiros, nem anúncios, nem SDKs de análise.

## O que o App armazena no seu dispositivo

- **Perfis.** Nome, emoji, cor e ajustes por perfil.
- **Estado de repetição espaçada.** Para cada cartão (ex.: `7 + 8`): data da próxima revisão, dificuldade, estabilidade e contagem de revisões.
- **Atividade.** Uma contagem diária de revisões concluídas por perfil (usada para a etiqueta de sequência e a tela de Estatísticas).
- **Erros.** Uma fila de problemas que você respondeu incorretamente recentemente, para que o App possa exibi-los de novo.
- **Preferências.** Opções de todo o App, como se a sincronização do iCloud está ativada.

Tudo isso é gravado na pasta Documentos isolada do próprio App e no `UserDefaults`. O App não pode ler os dados de outros apps, e outros apps não podem ler os dados do App.

## O que o App armazena opcionalmente no iCloud

A sincronização do iCloud fica **desativada por padrão**. Quando você a ativa (ícone de engrenagem → **Ajustes → Sincronização → Usar iCloud**), o App grava os mesmos dados descritos acima no seu iCloud privado por meio da API **CloudKit** da Apple. É o seu iCloud, acessível apenas por você nos dispositivos conectados com o mesmo ID Apple. Nós não temos acesso a ele.

- Os dados exatamente sincronizados: perfis, estados dos cartões, atividade, erros e (opcionalmente) os metadados de compartilhamento da família (um nome de exibição que você escolhe para sua família).
- A sincronização do iCloud **não** inclui o conteúdo de nenhuma gravação de voz nem nenhuma análise.
- Quando você entra com um ID Apple diferente, o App detecta a mudança e desativa a sincronização até que você a reative explicitamente, para que os dados não sejam enviados silenciosamente para outra conta.
- Excluir um perfil em **Gerenciar perfis** remove o perfil do dispositivo e (quando o iCloud está acessível no ID Apple original) também da sua cópia do iCloud.

## Compartilhamento da família

Na v3, o compartilhamento ocorre no nível da **família** em vez de por perfil. Abra o ícone de engrenagem → **Ajustes → Família → Configurar família**, dê um nome à sua família e convide familiares pela folha de compartilhamento padrão do iOS (Mensagens, Mail ou AirDrop).

- Todos os perfis no dispositivo do proprietário pertencem à família. Convidar um familiar compartilha todos de uma vez.
- Os dados ficam no **iCloud do proprietário da família**. Os participantes não armazenam uma cópia separada no próprio iCloud; a atividade de estudo deles é gravada diretamente no CloudKit do proprietário por meio do modelo de permissões CKShare com escopo de zona da Apple.
- Entrar em uma família é **destrutivo no dispositivo que entra**: os perfis locais existentes do participante são substituídos pelos da família. Antes de entrar, o App oferece a opção **Exportar perfis para arquivo** para que você salve uma cópia JSON dos seus dados atuais e a reimporte mais tarde se mudar de ideia.
- Se o proprietário encerrar a família (Ajustes → Família → Encerrar) ou sair do iCloud, os participantes perdem o acesso ao vivo na próxima sincronização. O cache local dos perfis da família passa a ser deles (sem exclusão destrutiva na saída).
- Um participante pode sair de uma família a qualquer momento (Ajustes → Família → Sair). Ao sair, mantém os perfis da família no dispositivo como próprios.
- O limite de `CKShare` da Apple é de 100 participantes por item compartilhado. A escala natural de uma família é de ~6.

## Exportar / Importar (backup JSON)

Em **Ajustes → Backup** você pode:

- **Exportar perfis para arquivo**: salvar um arquivo JSON contendo todos os perfis do dispositivo atual (qualquer estado da família). Útil como backup manual ou antes de operações destrutivas.
- **Importar perfis de arquivo**: restaurar uma exportação anterior. O modo **Mesclar** adiciona os perfis ausentes e atualiza os existentes se a cópia importada for mais recente. O modo **Substituir** apaga os perfis locais e instala o conjunto importado; disponível apenas quando você não está em uma família.

## Microfone e reconhecimento de fala

Quando o modo de voz está ativado, enquanto você responde a um problema o App:

1. Captura o áudio do microfone ao vivo com o `AVAudioEngine`.
2. Transmite-o para o `SFSpeechRecognizer` (o framework da Apple). Em dispositivos iOS modernos, o reconhecimento é executado no dispositivo por padrão; algumas configurações podem usar os servidores de reconhecimento de fala da Apple.
3. Lê os dígitos transcritos e avalia a resposta.
4. Para a captura assim que uma resposta final é obtida.

Não retemos áudio, transcrições nem qualquer sinal derivado. Não transmitimos áudio a nenhuma parte além do `SFSpeechRecognizer` da Apple. O App solicita `NSMicrophoneUsageDescription` e `NSSpeechRecognitionUsageDescription` no primeiro uso; se qualquer uma das permissões for negada, o modo de voz é desativado automaticamente e o teclado numérico na tela é usado.

## Registros de diagnóstico

O App emite eventos de diagnóstico não estruturados por meio do framework padrão `OSLog` da Apple (ex.: "sessão de estudo encerrada, corretas=12 erradas=3"). Esses registros:

- Permanecem no dispositivo.
- São visíveis apenas para você, no Console.app enquanto o dispositivo está conectado a um Mac.
- Usam a classificação de privacidade `.private` da Apple para qualquer valor potencialmente identificável (id de perfil, nome de perfil), de modo que esses valores são ocultados nas versões publicadas.

Não coletamos, recuperamos nem transmitimos o conteúdo do `OSLog`.

## Dados que NÃO coletamos

- Seu nome, e-mail ou dados de contato.
- Sua localização.
- Qualquer identificador de dispositivo (IDFA, IDFV, id de publicidade).
- Relatórios de falha além do que a Apple possa coletar por meio dos seus ajustes do iOS.
- Qualquer análise ou telemetria comportamental.
- Informações de pagamento ou cobrança (as compras são tratadas inteiramente pela Apple).

## Privacidade das crianças

O Mate Diária foi projetado para ser seguro para crianças. Como o App não coleta informações pessoais e não contata terceiros, ele atende à definição de "nenhuma informação pessoal" da COPPA. Não exibimos anúncios e não há contas nem recursos sociais. O Mate Diária inclui uma única compra dentro do app (um desbloqueio do app completo); como o app é projetado para crianças, uma verificação para adultos é exibida antes de qualquer compra, conforme exigem as regras da categoria Crianças da Apple. Todos os pagamentos e quaisquer resgates de código são tratados pela Apple por meio da App Store. O App nunca vê nem armazena seus dados de pagamento.

## Suas opções

- **Desativar o modo de voz** a qualquer momento por perfil (Ajustes → Modo de voz) ou globalmente negando a permissão do microfone nos Ajustes do iOS.
- **Desativar a sincronização do iCloud** a qualquer momento (ícone de engrenagem → Ajustes → Sincronização → Usar iCloud → desativado). Desativá-la não exclui as cópias do iCloud; exclua cada perfil individualmente se quiser removê-las.
- **Encerrar ou sair de uma família** (Ajustes → Família → Encerrar / Sair) para parar de compartilhar. Encerrar revoga o acesso dos participantes à sua família; sair mantém os perfis da família no seu dispositivo como próprios.
- **Exportar perfis para um arquivo** (Ajustes → Backup → Exportar) e mantê-lo localmente: um backup manual que nunca toca o iCloud.
- **Redefinir o progresso de um perfil** sem excluir o perfil (Ajustes do perfil → Redefinir).
- **Excluir um perfil** (Gerenciar perfis → deslize ou toque para excluir): também remove a cópia do iCloud quando a sincronização está ativada. Repita por perfil para remover tudo.

## Alterações nesta política

Se alterarmos esta política, a nova versão estará disponível na mesma URL com uma data de **Última atualização** atualizada. Mudanças significativas também serão indicadas nas notas de versão do App.

## Contato

Dúvidas sobre esta política ou seus dados? E-mail **spacedmath@gmail.com**.
