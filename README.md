🚀 Resumo do Lab: Governança e Conformidade no Microsoft Azure

## 📋 Visão Geral do Projeto
Este projeto explora as ferramentas e estratégias de governança, conformidade e proteção de dados no ecossistema Azure, abordando desde políticas automatizadas e bloqueios de recursos até monitoramento de compliance e governança de dados, alinhados aos conceitos da certificação AZ-900.

## 🎯 O que Aprendi

### **1. Azure Policy para Governança**
#### **Implementação de Políticas**
```
azurecli
# Listando políticas disponíveis
az policy definition list --query "[].{Name:name, DisplayName:displayName}" --output table

# Atribuindo política para exigir tags em recursos
az policy assignment create \
  --name 'require-tags-policy' \
  --policy 'Require a tag on resources' \
  --params '{"tagName": {"value": "Environment"}}'

  ```

  - **Propósito**: Enforcement de padrões organizacionais em escala

- **Avaliação Contínua**: Monitoramento automático de compliance

- **Definições Built-in**: +300 políticas pré-definidas categorizadas

- **Iniciativas**: Grupos de políticas relacionadas

### **Categorias de Políticas**
|	Categoria		|Exemplos de Políticas	|
|-------------------|-----------------------|
|	Segurança		|Exigir SSL enforcement, NSG rules	|
|	Custos			|Limitar tipos de VM, SKUs permitidas	|
|	Tags			|Exigir tags específicas em recursos	|
|	Conformidade	|Standards regulatórios (ISO, NIST, SOC)	|

## **2. Resource Locks (Bloqueios de Recursos)**
**Implementação de Locks**
```
azurecli

# Aplicando lock de delete em um resource group
az lock create \
  --name LockGroup \
  --lock-type CanNotDelete \
  --resource-group meu-rg-producao

# Listando locks existentes
az lock list --resource-group meu-rg-producao --output table

```
- **Proteção**: Prevenção contra exclusão ou modificação acidental

- **Níveis**: Subscription, Resource Group, Recurso individual

- **Tipos**: CanNotDelete (leitura permitida) vs ReadOnly (nenhuma modificação)

- **Governança**: Controle de mudanças em ambientes críticos

## **3. Service Trust Portal**
**Acesso e Recursos**
```
bash
# Portal para documentação de compliance e segurança
# https://servicetrust.microsoft.com/

```
- **Documentação**: Relatórios de compliance detalhados

- **Auditorias**: Resultados de auditorias independentes

- **Políticas**: Informações de segurança e privacidade

- **Transparência**: Insights sobre operações Microsoft

4. Microsoft Purview para Governança de Dados
Implementação de Data Governance
azurecli
# Criando uma conta do Purview (exemplo conceitual)
```
az purview account create \
  --name minha-conta-purview \
  --resource-group meu-rg-governance \
  --location eastus

  ```
- **Unified Data Governance**: Visão única across multicloud e on-premises

- **Data Discovery**: Descoberta automática de dados sensíveis

- **Data Classification**: Classificação automatizada baseada em sensibilidade

- **Data Lineage**: Rastreamento completo de linhagem de dados

### **Funcionalidades do Purview**
|	Funcionalidade	|	Benefício	|
|-------------------|---------------|
|	Data Map		|	Catálogo de dados automatizado	|
|	Data Catalog	|	Descoberta e colaboração	|
|	Data Insights	|	Analytics de dados sensíveis	|
|	Data Policy		|	Enforcement de políticas de dados	|


## **5. Azure Blueprints**
### **Orquestração de Governança**
```
json
// Exemplo de blueprint (conceitual)
{
  "version": "1.0",
  "resources": {
    "policies": ["require-tags", "allowed-vm-skus"],
    "roleAssignments": ["contributor", "reader"],
    "resourceGroups": ["network-rg", "storage-rg"]
  }
}

```
- **Packaging**: Empacotamento de artefatos de governança

- **Versioning**: Controle de versão de environments

- **Deployment**: Implantação consistente de recursos

- **Compliance**: Tracking de conformidade por blueprint

## **🛠️ Ferramentas e Serviços Utilizados**
- **Azure Policy**

- **Resource Locks**

- **Service Trust Portal**

- **Microsoft Purview**

- **Azure Blueprints**

- **Azure CLI e PowerShell**

- **Azure Governance Visualizer**

## **📊 Matriz de Governança Azure**
|	Camada		|Ferramenta			|Propósito	|
|---------------|-------------------|-----------|
|	Preventiva	|Azure Policy		|Enforcement de standards	|
|	Protetiva	|Resource Locks		|Prevenção de alterações	|
|	Detectiva	|Azure Monitor		|Detecção de não-conformidade	|
|	Corretiva	|Azure Automation	|Remediação automática	|

## **🔧 Implementações Práticas**
**Política para Exigir Tags**
```
azurecli
# Criando política personalizada para tags
az policy definition create \
  --name 'require-environment-tag' \
  --display-name 'Require Environment tag' \
  --description 'This policy requires an Environment tag on all resources.' \
  --rules '{
    "if": {
      "field": "tags[Environment]",
      "exists": false
    },
    "then": {
      "effect": "deny"
    }
  }'

  ```
### **Lock em Recursos Críticos**

```
bash
# Aplicando lock read-only em VMs de produção
az lock create --name LockVM --lock-type ReadOnly --resource-group production-rg --resource-name my-vm --resource-type Microsoft.Compute/virtualMachines
```

### **🚦 Principais Desafios e Soluções**
|Desafio							|Solução Implementada	|
|-----------------------------------|-----------------------|
|Compliance em Scale				|Azure Policy com iniciativas built-in	|
|Proteção de Recursos Críticos		|Resource Locks em múltiplos níveis	|
|Governança de Dados				|Microsoft Purview para descoberta e classificação	|
|Transparência de Segurança			|Service Trust Portal para documentação	|
|Implementação Consistente			|Azure Blueprints para environments	|

## **📈 Melhores Práticas Aplicadas**
1. **Policy-Driven Governance**: Tudo como código (policy as code)

2. **Least Privilege**: Locks apenas onde necessário

3. **Data Classification**: Classificação automática de dados sensíveis

4. **Continuous Compliance**: Monitoramento contínuo de conformidade

5. **Documentation**: Service Trust Portal para transparência

## **💡 Casos de Uso Implementados**
- **Ambiente Regulado**: Políticas para compliance HIPAA/SOC2

- **Recursos Críticos**: Locks em databases de produção

- **Governança de Dados**: Purview para catalogação de dados sensíveis

- **Implementação Padrão**: Blueprints para novos environments

## **🔗 Links Úteis e Materiais de Apoio**
[Azure Policy Documentation](https://learn.microsoft.com/azure/governance/policy/)

[Microsoft Purview Documentation] (https://learn.microsoft.com/purview/)

[Service Trust Portal](https://servicetrust.microsoft.com/)

[Azure Governance Framework](https://learn.microsoft.com/azure/cloud-adoption-framework/govern/)

[Slides do Curso - Governança e Conformidade](https://web.dio.me/track/formacao-microsoft-az-900-certification/course/governanca-e-conformidade/learning/a5463253-0353-4bde-ab8d-381f90a3901a?autoplay=1)

## **🌐 Framework de Governança**
**Azure Policy**: Enforcement de standards

**Azure Blueprints**: Ambiente packaging

**Microsoft Purview**: Governança de dados

**Resource Locks**: Proteção de recursos

**Service Trust**: Transparência e compliance

## 📝 Conclusão e Insights
O laboratório proporcionou uma visão abrangente do ecossistema de governança Azure:

- Governança automatizada é essencial em escala cloud
- Políticas preventivas evitam problemas antes que ocorram
- A transparência do Service Trust Portal fortalece a confiança
- Microsoft Purview resolve desafios complexos de governança de dados
- Resource Locks protegem recursos críticos de alterações acidentais

## 🎯 Próximos Passos de Aprendizado
- [ ] Explorar Azure Blueprints para orquestração de ambientes
- [ ] Aprofundar em Microsoft Purview Data Catalog
- [ ] Estudar Azure Regulatory Compliance
- [ ] Aprender Azure Management Groups para hierarquia
- [ ] Certificação SC-900 (Security, Compliance, Identity)

---

*Desenvolvido como parte do Bootcamp Formação Microsoft AZ-900 Certification na DIO*

![Azure Governance](https://img.shields.io/badge/Azure-Governance-blue)
![Compliance](https://img.shields.io/badge/Compliance-Regulatory-green)
![Microsoft Purview](https://img.shields.io/badge/Data-Purview-purple)
![AZ-900](https://img.shields.io/badge/Certification-AZ--900%20Fundamentals-success)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)
![DIO](https://img.shields.io/badge/Platform-DIO-orange)

## 📞 Suporte e Comunidade
- [Fórum DIO - Governança Azure](https://web.dio.me/articles)
- [Microsoft Governance Community](https://techcommunity.microsoft.com/t5/azure-governance/bg-p/AzureGovernance)
- [Azure Policy GitHub](https://github.com/Azure/azure-policy)

---

## 🔍 Exemplos de Políticas Comuns

### **Política de Tags Obrigatórias**
```json
{
  "mode": "All",
  "policyRule": {
    "if": {
      "field": "tags",
      "exists": "false"
    },
    "then": {
      "effect": "deny"
    }
  }
}
```