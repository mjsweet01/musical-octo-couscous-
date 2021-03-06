---
title: グループを使用してセルフホストランナーへのアクセスを管理する
intro: ポリシーを使用して、Organization または Enterprise に追加されたセルフホストランナーへのアクセスを制限できます。
redirect_from:
  - /actions/hosting-your-own-runners/managing-access-to-self-hosted-runners
versions:
  free-pro-team: '*'
  enterprise-server: '>=2.22'
  github-ae: '*'
type: tutorial
---

{% data reusables.actions.ae-self-hosted-runners-notice %}
{% data reusables.actions.enterprise-beta %}
{% data reusables.actions.enterprise-github-hosted-runners %}
{% data reusables.actions.ae-beta %}

### セルフホストランナーのグループについて

{% if currentVersion == "free-pro-team@latest" %}
{% note %}

**注釈:** すべての Organization には、単一のデフォルトのセルフホストランナーグループがあります。 追加のセルフホストランナーグループの作成と管理は、Enterprise アカウント、および Enterprise アカウントが所有する Organization でのみ使用できます。

{% endnote %}
{% endif %}

セルフホストランナーグループは、Organization レベルおよび Enterprise レベルでセルフホストランナーへのアクセスを制御するために使用されます。 Enterprise の管理者は、Enterprise 内のどの Organization がランナーグループにアクセスできるかを制御するアクセスポリシーを設定できます。 Organization の管理者は、Organization 内のどのリポジトリがランナーグループにアクセスできるかを制御するアクセスポリシーを設定できます。

Enterprise の管理者が Organization にランナーグループへのアクセスを許可すると、Organization の管理者は、Organization のセルフホストランナー設定にリストされたランナーグループを表示できます。 Organization の管理者は、追加の詳細なリポジトリアクセスポリシーを Enterprise ランナーグループに割り当てることができます。

新しいランナーが作成されると、それらは自動的にデフォルトグループに割り当てられます。 ランナーは一度に1つのグループにのみ参加できます。 ランナーはデフォルトグループから別のグループに移動できます。 詳しい情報については、「[セルフホストランナーをグループに移動する](#moving-a-self-hosted-runner-to-a-group)」を参照してください。

### Organization のセルフホストランナーグループを作成する

すべての Organization には、単一のデフォルトのセルフホストランナーグループがあります。 Enterprise アカウント内の Organization は、追加のセルフホストグループを作成できます。 Organization の管理者は、個々のリポジトリにランナーグループへのアクセスを許可できます。

セルフホストランナーは、作成時にデフォルトグループに自動的に割り当てられ、一度に 1 つのグループのメンバーになることができます。 ランナーはデフォルトグループから作成した任意のグループに移動できます。

グループを作成する場合、ランナーグループにアクセスできるリポジトリを定義するポリシーを選択する必要があります。

{% data reusables.organizations.navigate-to-org %}
{% data reusables.organizations.org_settings %}
{% data reusables.github-actions.settings-sidebar-actions-runners %}
1. {% if currentVersion == "free-pro-team@latest" %}[Runners]{% else %}[Self-hosted runners]{% endif %} セクションで、[**Add new**]、[**New group**] の順にクリックします。

    ![新しいランナーを追加](/assets/images/help/settings/actions-org-add-runner-group.png)
1. ランナーグループの名前を入力し、リポジトリアクセスのポリシーを割り当てます。

   {% if currentVersion == "free-pro-team@latest" or currentVersion ver_gt "enterprise-server@2.22" or currentVersion == "github-ae@latest" %} リポジトリの特定のリスト、または Organization 内のすべてのリポジトリにアクセスできるようにランナーグループを設定できます。 デフォルトでは、プライベートリポジトリのみがランナーグループ内のランナーにアクセスできますが、これをオーバーライドできます。{% elsif currentVersion == "enterprise-server@2.22"%} リポジトリの特定のリスト、すべてのプライベートリポジトリ、または Organization 内のすべてのリポジトリにアクセスできるようにランナーグループを設定できます。{% endif %}

   {% warning %}

   **Warning**

   {% indented_data_reference reusables.github-actions.self-hosted-runner-security spaces=3 %}

   詳しい情報については「[セルフホストランナーについて](/actions/hosting-your-own-runners/about-self-hosted-runners#self-hosted-runner-security-with-public-repositories)」を参照してください。

   {% endwarning %}

   ![ランナーグループのオプションを追加](/assets/images/help/settings/actions-org-add-runner-group-options.png)
1. [**Save group**] をクリックしてグループを作成し、ポリシーを適用します。

### Enterprise のセルフホストランナーグループを作成する

Enterprise は、セルフホストランナーをグループに追加して、アクセス管理を行うことができます。 Enterprise は、Enterprise アカウント内の特定の Organization がアクセスできるセルフホストランナーのグループを作成できます。 Organization の管理者は、追加の詳細なリポジトリアクセスポリシーを Enterprise ランナーグループに割り当てることができます。

セルフホストランナーは、作成時にデフォルトグループに自動的に割り当てられ、一度に 1 つのグループのメンバーになることができます。 登録処理中にランナーを特定のグループに割り当てることも、後でランナーをデフォルトグループからカスタムグループに移動することもできます。

グループを作成するときは、ランナーグループにアクセスできる Organization を定義するポリシーを選択する必要があります。

{% data reusables.enterprise-accounts.access-enterprise %}
{% data reusables.enterprise-accounts.policies-tab %}
{% data reusables.enterprise-accounts.actions-tab %}
{% data reusables.enterprise-accounts.actions-runners-tab %}
1. [**Add new**] をクリックしてから、[**New group**] をクリックします。

    ![新しいランナーを追加](/assets/images/help/settings/actions-enterprise-account-add-runner-group.png)
1. ランナーグループの名前を入力し、Organization アクセスのポリシーを割り当てます。

   {% if currentVersion == "free-pro-team@latest" or currentVersion ver_gt "enterprise-server@2.22" or currentVersion == "github-ae@latest" %} ランナーグループを設定して、特定の Organization のリスト、または Enterprise 内のすべての Organization にアクセスできるようにすることができます。 デフォルトでは、プライベートリポジトリのみがランナーグループ内のランナーにアクセスできますが、これをオーバーライドできます。{% elsif currentVersion == "enterprise-server@2.22"%} Enterprise 内のすべての Organization がアクセスできるようにランナーグループを設定することも、特定の Organization を選択することもできます。{% endif %}

   {% warning %}

   **Warning**

   {% indented_data_reference reusables.github-actions.self-hosted-runner-security spaces=3 %}

   詳しい情報については「[セルフホストランナーについて](/actions/hosting-your-own-runners/about-self-hosted-runners#self-hosted-runner-security-with-public-repositories)」を参照してください。

   {% endwarning %}

    ![ランナーグループのオプションを追加](/assets/images/help/settings/actions-enterprise-account-add-runner-group-options.png)
1. [**Save group**] をクリックしてグループを作成し、ポリシーを適用します。

### セルフホストランナーグループのアクセスポリシーを変更する

ランナーグループのアクセスポリシーを更新したり、ランナーグループの名前を変更したりすることができます。

{% data reusables.github-actions.self-hosted-runner-configure-runner-group-access %}

### セルフホストランナーをグループに移動する

新しいセルフホストランナーは自動的にデフォルトグループに割り当てられ、その後、別のグループに移動できます。

1. {% if currentVersion == "free-pro-team@latest" %}[Runners]{% else %}[Self-hosted runners]{% endif %} セクションで、移動するランナーの現在のグループを見つけて、グループメンバーのリストを展開します。 ![ランナーグループのメンバーを表示](/assets/images/help/settings/actions-org-runner-group-members.png)
1. セルフホストランナーの横にあるチェックボックスを選択し、[**Move to group**] をクリックして、利用可能な移動先を確認します。 ![ランナーグループのメンバーを移動](/assets/images/help/settings/actions-org-runner-group-member-move.png)
1. 移動先のグループをクリックして、ランナーを移動します。 ![ランナーグループのメンバーを移動](/assets/images/help/settings/actions-org-runner-group-member-move-destination.png)

### セルフホストランナーグループを削除する

セルフホストランナーは、グループが削除されると自動的にデフォルトグループに戻ります。

1. 設定ページの {% if currentVersion == "free-pro-team@latest" %}[Runners]{% else %}[Self-hosted runners]{% endif %} セクションで、削除するグループを見つけて、{% octicon "kebab-horizontal" aria-label="The horizontal kebab icon" %} ボタンをクリックします。 ![ランナーグループの設定を表示](/assets/images/help/settings/actions-org-runner-group-kebab.png)

1. グループを削除するには、[**Remove group**] をクリックします。 ![ランナーグループの設定を表示](/assets/images/help/settings/actions-org-runner-group-remove.png)

1. 確認プロンプトを確認し、[**Remove this runner group**] をクリックします。
