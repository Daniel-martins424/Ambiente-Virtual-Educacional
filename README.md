# __Script em Batch: Desafio de Automação__
## calendário

![Imagem](https://sme.goiania.go.gov.br/conexaoescola/wp-content/uploads/2023/04/1-10-e1682602359525.jpg)

__Descrição:__ 

![Imagem](https://scontent.fcpq1-1.fna.fbcdn.net/v/t1.15752-9/479302579_659759359752187_5204559823626069491_n.png?_nc_cat=100&ccb=1-7&_nc_sid=0024fc&_nc_ohc=0RhfnhazoTcQ7kNvgFNeXiC&_nc_oc=AdgNdyZNPOtlsp7lmF_oIpzEmWyzES-XTRNPdBoeLE8J0NiSj3riBaL1GYTX2WjNoSw&_nc_ad=z-m&_nc_cid=0&_nc_zt=23&_nc_ht=scontent.fcpq1-1.fna&oh=03_Q7cD1gG7DohJjXjjX_2LxK9Ip7z6rjUE_e1ahguIX_7sywKFxw&oe=67DE9E45)

- Este script em Batch (calendario.bat) cria diretórios com base no ano e mês fornecidos como argumentos.

## __Resumo do funcionamento:__

__Criação de diretórios:__

Se a pasta do primeiro argumento (%1%) não existir, ela é criada e acessada.
O mesmo ocorre para o segundo argumento (%2%).
Cálculo de dias do mês:

Determina se o ano é bissexto.
Define a quantidade de dias do mês informado (mes=%2).
Se for fevereiro (2), ajusta para 28 ou 29 dias, conforme o ano.
Outros meses são configurados corretamente (30 ou 31 dias).
Criação de diretórios numerados de 1 até o total de dias do mês.

Retorno ao diretório anterior (cd ..).

__O script essencialmente organiza pastas para representar um calendário mensal com os dias numerados.__


## __Comandos Utilizados:__

- @ECHO off

__Oculta a exibição dos comandos no terminal, mostrando apenas a saída.__

- if not exist "caminho" mkdir "caminho"

__Verifica se um diretório existe (if not exist); se não existir, cria (mkdir).__

- cd "caminho"

__Muda o diretório atual para o especificado.__

- set variavel=valor

__Define uma variável com um valor específico.__

- set /a variavel=expressão

__Atribui a uma variável o resultado de uma expressão matemática.__

- if condição (comando)

__Executa um comando caso a condição seja verdadeira.__

- if condição (bloco de comandos) else (outro bloco)


__Estrutura condicional que executa um bloco de comandos se a condição for verdadeira, senão executa outro.__

- for /L %%variavel in (início, incremento, fim) do (comandos)

__Laço de repetição que executa comandos em um intervalo de números.__

- echo mensagem

__Exibe uma mensagem no terminal.__

- cd ..
__Retorna ao diretório anterior.__

## Explicação da programação:
1. __@ECHO off__

Função no script:
Oculta a exibição dos comandos no terminal, deixando a saída mais limpa.

2. __if not exist "%1" mkdir "%1"__

Função no script:
Verifica se o diretório correspondente ao primeiro argumento (%1 - ano) existe.
Se não existir, cria a pasta com mkdir "%1".

3. __cd "%1"__

Função no script:
Entra no diretório criado ou existente para organizar os meses dentro dele.

4. __f not exist "%2" mkdir "%2"__

Função no script:
Verifica se o diretório do segundo argumento (%2 - mês) existe.
Se não existir, cria a pasta do mês.

5. __cd "%2"__

Função no script:
Entra no diretório do mês para criar os dias dentro dele.

6. __Definição de variáveis (set)__

batch
Copiar
Editar
set /a ano=%1
set /a bissexto=%ano% %% 4
set /a seculo=%ano% %% 100
set /a quadricentenario=%ano% %% 400
Função no script:
ano=%1 → Armazena o ano fornecido como argumento.
bissexto=%ano% %% 4 → Calcula o resto da divisão do ano por 4 para verificar se pode ser bissexto.
seculo=%ano% %% 100 → Calcula o resto da divisão do ano por 100 para verificar se é um século.
quadricentenario=%ano% %% 400 → Calcula o resto da divisão do ano por 400 para confirmar se é bissexto.

7. __Definição do mês__
batch
Copiar
Editar

set mes=%2
Função no script:
Armazena o número do mês informado.

8. __Definição do número de dias no mês__
batch
Copiar
Editar
if %mes%==1 set dias=31
if %mes%==2 set dias=28
Função no script:
Define os dias de cada mês.
Se for janeiro (1), define 31 dias.
Se for fevereiro (2), inicialmente assume 28 dias (caso o ano não seja bissexto).

9. __Verificação de ano bissexto para fevereiro__


if %mes%==2 (

    if %bissexto%==0 (

        if not %seculo%==0 (

            set dias=29

        ) else if %quadricentenario%==0 (

            set dias=29

        )

    )

)

Função no script:
Se o mês for fevereiro (%mes%==2), verifica se o ano é bissexto.
Regras:
Se o ano for divisível por 4 (bissexto%==0) e não for um século (%seculo%!=0), define 29 dias.

Se for um século (%seculo%==0), só será bissexto se também for divisível por 400 (quadricentenario%==0).

10. __Definição de dias para os demais meses__


if %mes%==3 set dias=31

if %mes%==4 set dias=30

if %mes%==5 set dias=31

if %mes%==6 set dias=30

if %mes%==7 set dias=31

if %mes%==8 set dias=31

if %mes%==9 set dias=30

if %mes%==10 set dias=31

if %mes%==11 set dias=30

if %mes%==12 set dias=31

Função no script:
Define a quantidade de dias de cada mês do ano.
Meses com 31 dias: Janeiro, março, maio, julho, agosto, outubro e dezembro.
Meses com 30 dias: Abril, junho, setembro e novembro.

11. __Exibir a quantidade de dias do mês__

echo este mes tem %dias% dias

Função no script:
Exibe a quantidade de dias definida para o mês no terminal.

12. __Criar diretórios numerados de 1 até o número de dias do mês__


for /L %%i in (1,1,%dias%) do (

    if not exist %%i (

        mkdir %%i

    )

)

Função no script:
for /L %%i in (1,1,%dias%) → Laço de repetição que percorre de 1 até o último dia do mês (%dias%).

if not exist %%i ( mkdir %%i ) → Para cada número, verifica se a pasta já existe; se não, cria.

13. __Retornar ao diretório anterior__

cd ..

cd ..

Função no script:
Sai da pasta do mês (cd ..).
Sai da pasta do ano (cd ..).

Resumo Geral

Cria uma pasta com o nome do ano (%1).

Cria uma pasta com o nome do mês (%2) dentro dela.

Calcula a quantidade de dias do mês, considerando ano bissexto.

Cria pastas numeradas de 1 até o número de dias do mês dentro da pasta do mês.

Sai da pasta e retorna ao diretório original.


