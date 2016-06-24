# Design atividade SignAC
- Data: 24/06/2016
- Autores: Jonathan / Pedro

___
## Myrp

### Renomear aba Varejo/NFCe para "NFC-e / S@T CF-e" (confirmar nome)
- Projeto: Gerencial
  - renomear nome da aba no arquivo **empresa/form.cshtml**
 
### Sempre mostrar aba NFC-e / S@at CF-e
- Projeto: Gerencial
  - arquivo **empresa\formempresa.js** 
    - remover/tratar controleExibicaoAbaVarejo
	- tratar exibição de novos campos/componentes no método exibirAbasEdocs (assim como é feito com o CTe e MDFe)

### Incluir campo SignAC no cadastro da empresa, na nova aba "NFC-e / S@T CF-e"
- Projeto: Varejo
  - incluir campo SignAC na entidade Empresa.cs
    - incluir campo no mapeamento EmpresaMap.cs
	- criar script para criação do campo na tabela EMPRESA (databases\varejo\aamm\nome do script)
  - incluir campo SignAC na tela
    - deve haver descrição sobre o campo e links para o blog (ajuda)
	- view model EmpresaViewModel (campo será obrigatório se empresa possui S@T e não apresentado se não possui S@T)
	- caso ainda não gerado deve mostrar o botão "Gerar"
	- caso já foi gerado, deve mostrar o campo (não editável) com o botão "Copiar"
  - Gerar SignAC
    - incluir botão que ao clicado gera o SignAC (utilizando DLL externa), atualiza o campo no banco e mostra-o na tela

### Integrar SignAC com o Barramento
- criar script atualizando a view ERPIntegracoes.dbo.INTERF_CONFIGURACOES_EMITENTE adicionando o campo SignAC (databases\varejo\aamm\nome do script)

### Criar item na lista de pendências do dashboard
- Projeto: App
  - incluir campo de pendencia de SignAC em **pendenciasEmissao.html**
  - incluir campo de pendencia de SignAC em **pendenciasEmissao.js**
- Projeto: ApiGateway
  - incluir tratamento da pendencia SignAC nos arquivos **PendenciasEmissaoFiscalController.cs** e **PendenciasEmissaoFiscalViewModel**
    - somente possui pendência SignAC se empresa possui módulo varejo e possui S@T
  - alterar o comunicador **Varejo\ComunicadorEmpresa***
    - renomear metodo EmpresaDaSessaoPossuiCadastroCompletoAsync para ObterEmpresaDaSessaoAsync que deve retornar a classe **EmpresaVarejoDto** (que deve ser criada)
    - criar class EmpresaVarejoDto contendo os campos CompletouCadastro e PossuiSignAC
- Projeto: Varejo
  - ajustar retorno do controller ERP.Varejo.Web.Areas.APIGateway.Controllers.EmpresaController para retornar os dados CompletouCadastro e SignAC
  - após gerar o SignAC, deve voltar para dashboard (somente se houver o parametro retornar)


  
  
___
## PDV

### Receber SignAC via integração
- Falta análise



___
## Gerador SignAC

### Dado o CNPJ do cliente, deve gerar o SignAC


### Criar testes no CI para validar a validade do certificado da Inventti - quando faltar menos de 20 dias para o certificado vencer, deve falhar


### Deve ter uma configuração para configurar o path e senha do certificado


### Não deve-se comitar o arquivo de configuração no repositorio


### Publicar solução via DLL


