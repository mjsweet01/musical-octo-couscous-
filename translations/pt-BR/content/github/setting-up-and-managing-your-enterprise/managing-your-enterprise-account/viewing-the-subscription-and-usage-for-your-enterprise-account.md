---
title: Exibir assinatura e uso da conta corporativa
intro: 'Você pode exibir a assinatura atual, o uso da licença, as faturas, o histórico de pagamentos e outras informações de cobrança da sua conta corporativa.'
product: '{% data reusables.gated-features.enterprise-accounts %}'
permissions: Enterprise owners and billing managers can access and manage all billing settings for enterprise accounts.
redirect_from:
  - /github/setting-up-and-managing-your-enterprise-account/viewing-the-subscription-and-usage-for-your-enterprise-account
  - /articles/viewing-the-subscription-and-usage-for-your-enterprise-account
  - /github/setting-up-and-managing-your-enterprise/viewing-the-subscription-and-usage-for-your-enterprise-account
versions:
  free-pro-team: '*'
  enterprise-server: '*'
topics:
  - Enterprise
---

### Sobre a cobrança de contas corporativas

As contas corporativas atualmente estão disponíveis para clientes do {% data variables.product.prodname_enterprise %} que pagam com fatura. As cobranças para todas as organizações e instâncias de {% data variables.product.prodname_ghe_server %} conectadas à sua conta corporativa são agregadas em uma única taxa de conta para todos os seus serviços de {% data variables.product.prodname_dotcom_the_website %} pelos quais você pagou (incluindo licenças pagas nas organizações, {% data variables.large_files.product_name_long %} pacotes de dados{% if currentVersion == "free-pro-team@latest" or ver_gt "enterprise-server@3.0" %} {% data variables.product.prodname_GH_advanced_security %} uso,{% endif %} e assinaturas para aplicativos de {% data variables.product.prodname_marketplace %}).

{% if currentVersion == "free-pro-team@latest" %}{% data reusables.enterprise-accounts.billing-microsoft-ea-overview %} Para obter mais informações, consulte "[Conectar uma assinatura do Azure à sua empresa](/github/setting-up-and-managing-your-enterprise/connecting-an-azure-subscription-to-your-enterprise){% endif %}

Para obter mais informações sobre como administrar gerentes de cobrança, consulte "[Convidar pessoas para gerenciar a sua empresa](/github/setting-up-and-managing-your-enterprise/inviting-people-to-manage-your-enterprise)".

### Exibir assinatura e uso da conta corporativa

{% data reusables.enterprise-accounts.access-enterprise %}
{% data reusables.enterprise-accounts.settings-tab %}
{% data reusables.enterprise-accounts.license-tab %}
1. Em "{% if currentVersion == "free-pro-team@latest" %}Licenças do usuário{% else %}Licenças {% endif %}", veja seu total de licenças, número de licenças consumidas e a data de expiração da assinatura.
  {% if currentVersion == "free-pro-team@latest" %}![License and subscription information in enterprise billing settings](/assets/images/help/business-accounts/billing-license-info.png){% else %}
  ![Informações de assinaturas e licenças nas configurações de cobrança da empresa](/assets/images/enterprise/enterprise-server/enterprise-server-billing-license-info.png){% endif %}
1. Opcionalmente, para visualizar os detalhes para o uso da licença ou para fazer o download de um arquivo {% if currentVersion == "free-pro-team@latest" %}CSV{% elsif enterpriseServerVersions contains currentVersion %}JSON{% endif %} com detalhes da licença{% if currentVersion == "free-pro-team@latest" %}, à direita de "LIcenças do usuário" {% endif %}, clique em **Visualizar {% if currentVersion == "free-pro-team@latest" %}detalhes{% elsif enterpriseServerVersions contains currentVersion %}usuários{% endif %}** ou {% if currentVersion == "free-pro-team@latest" %}{% octicon "download" aria-label="The download icon" %}{% elsif enterpriseServerVersions contains currentVersion %}**Exportar uso da licença**{% endif %}.{% if currentVersion == "free-pro-team@latest" %} !["View details" button and button with download icon to the right of "User Licenses"](/assets/images/help/business-accounts/billing-license-info-click-view-details-or-download.png){% endif %}
{% if currentVersion == "free-pro-team@latest" or ver_gt "enterprise-server@3.0" %}
1. Opcionalmente, para visualizar os detalhes de uso para outras funcionalidades, clique em **Cobrança**. ![Aba de faturamento na barra lateral de configurações da conta corporativa](/assets/images/help/business-accounts/settings-billing-tab.png)

### Leia mais

- "[Sobre cobrança para o GitHub Actions](/billing/managing-billing-for-github-actions/about-billing-for-github-actions#about-billing-for-github-actions)"
- "[Sobre a cobrança para o Large Files Storage do Git](/billing/managing-billing-for-git-large-file-storage/about-billing-for-git-large-file-storage)"
- "[Sobre o licenciamento para {% data variables.product.prodname_GH_advanced_security %}](/billing/managing-licensing-for-github-advanced-security/about-licensing-for-github-advanced-security)"

{% endif %}
