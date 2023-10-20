**Hébergement Cloud vs On premises : quelle est la meilleure option pour l’environnement?**

On me demande souvent si, d'un point de vue environnemental, l'hébergement dans le Cloud est préférable à un hébergement "on premises". Vous devez vous en douter, la réponse n'est pas si simple à donner car cela dépend énormément du contexte.

Je vais tenter, ici, de donner un maximum d'informations pour alimenter la réflexion sur le sujet, tout en restant synthétique.

 

 

Pour commencer, il ne faut évidemment pas prendre pour argent comptant les économies d'émissions de GES promises par les principaux CSP (Cloud Service Provider). Boavizta a écrit [un très bon article que je vous invite à lire sur ce sujet](https://boavizta.org/blog/les-reductions-d-emissions-de-co2-promises-par-les-cloud-providers-sont-elles-realistes).

 

Malgré les promesses “légèrement” trompeuses des CSP qui communiquent sur le sujet, les principes du Cloud devraient naturellement rendre les services numériques qui y sont hébergés moins impactants (à périmètre constant) que s’ils étaient hébergés  "on premises", notamment pour les raisons suivantes :

 



1. **Mutualisation**

    La mutualisation permet, **à besoin constant**, de réduire la quantité de matériel et d'énergie nécessaires pour exécuter les services hébergés mais aussi les ressources humaines et donc les déplacements des équipes techniques.


    Plus le niveau de mutualisation est élevé, meilleure est la répartition des pics de charge. Cela permet donc d’éviter de dimensionner l’infrastructure pour gérer tous les pics de charge simultanément. Sur les infrastructures “on premises”, ce n’est pas possible car chaque client doit se mettre en capacité de gérer ses propres pics de charge.


    Les CSP utilisent aussi des services réseaux distribués sur les nœuds des clusters de compute plutôt que sur des équipements dédiés à cet effet. Cela leur permet de standardiser au maximum et de mutualiser encore plus car ils ont besoin de beaucoup moins d’équipements spécifiques.

2. **Business model des CSP**

    Les CSP ont tout intérêt à consommer le moins possible de ressources physiques et d'énergie, car c'est ce qui leur permet de rester compétitifs et d'optimiser leur rentabilité. On pourrait dire que les entreprises hébergeant "on premises" ont le même souci d'optimisation des coûts mais vu leur faible volume, ce n'est pas rentable pour elles d'embaucher les ressources humaines et de développer les outils nécessaires à cette optimisation.

3. **Recyclage / Réemploi**

    La plupart des CSP ont mis en place des process de recyclage et réemploi du matériel qui n'existent pas dans le monde de l'hébergement "on premises" où le matériel est, au mieux, vendu à un broker qui se chargera de lui trouver une seconde vie, très souvent dans des conditions d'utilisation pas du tout optimisées (sous utilisation et hébergement dans des locaux peu adaptés avec des PUE élevés). Les CSP, quant à eux, sont en mesure de réutiliser tout ou partie d'un équipement pour fournir un autre service et lorsque le matériel arrive vraiment en fin de vie, il part réellement vers une filière de recyclage.

4. **Efficacité des mécanismes de redondance**

    La gestion de la redondance et de la haute disponibilité est bien plus efficace chez un CSP qui répartit ses infrastructures sur au moins 3 zones de disponibilité (nécessité d'avoir 33% des ressources inutilisées, en mode nominal, pour palier à la perte d'un site) alors que très peu de sociétés faisant de l'hébergement "on premises" arrivent à aller au-delà de 2 sites (nécessité d'avoir 50% des ressources inutilisées en mode nominal pour palier à la panne d'un site).


    La gestion de la haute disponibilité interne à un seul site (pour gérer les cas de panne simple) est, elle aussi, optimisée dans le cloud par rapport aux infrastructures “on premises” car les volumétries à gérer sont beaucoup plus faibles “on premises” et cela nécessite un pourcentage d'équipements dédiés à la haute disponibilité beaucoup plus important. Pour illustrer mon propos, sur la plupart des infrastructures “on premises”, les équipements réseaux et sécurité sont généralement doublés (au moins sur le site principal mais aussi très souvent sur le site de secours) car la volumétrie de trafic ne requiert pas de gérer la répartition de charge sur plusieurs équipements. On a donc un équipement servant à gérer les cas de panne simple pour un équipement réellement utile. Cet équipement doit aussi être surdimensionné pour gérer la scalabilité verticale alors que les CSP répartissent ces services sur beaucoup plus d’équipements pour avoir un ratio _Nombre d’équipements utiles / Nombre total d’équipements_ beaucoup plus élevé. ![Exemple de gestion de la redondance sur une infrastructure “on premises”](./cloud%20vs%20onprem%201.png)
    Exemple de gestion de la redondance sur une infrastructure “on premises”
    
    ![Exemple de gestion de la redondance sur une infrastructure Cloud](./cloud%20vs%20onprem%202.png)Exemple de gestion de la redondance sur une infrastructure Cloud


    Les 2 schémas ci-dessus sont volontairement très simplifiés pour illustrer les principes sans entrer dans des détails d’architecture qui susciteraient trop de débats car il y a beaucoup trop de variables et donc d’hypothèses à prendre pour comparer une véritable architecture “on premises” avec une architecture de CSP.


    A noter qu’il est aussi fréquent d’avoir du matériel de “spare” en stock pour remplacer un équipement défaillant en cas de panne. Là aussi, la concentration et la standardisation des CSP permettent des économies de matériel.

5. **Nouvelles pratiques offertes par l'élasticité**

    L'élasticité du Cloud public permet d'envisager des économies qui n'avaient pas lieu d'être "on premises" puisque les infrastructures étaient prévues pour la capacité maximale d'utilisation (très peu utile donc d'éteindre les services, surtout dans un pays comme la France où le mix électrique est fortement décarbonné). Cela permet par exemple d'éteindre tous les environnements de build lorsqu'ils ne sont pas utilisés ou de les déployer dynamiquement sur des régions ou le mix électrique est moins carboné (équivalent à réseau électrique moins stressé). Cela est d'autant plus vrai pour des traitements nécessitant de très grosses capacités de compute et de stockage comme le Machine Learning. Si on avait à gérer ces traitements sur des infrastructures “on premises”, cela nécessiterait d'acheter énormément de hardware qui serait sous utilisé et cela pourrait même amener à un effet rebond puisqu'on aurait tendance à imaginer de nouveaux usages, pas forcément indispensables, pour utiliser ces ressources inutilisées la plupart du temps.

6. **Outillage clé en main**

    Les CSP offrent aujourd'hui une importante gamme d'outils clé en main, que cela soit pour gérer la sécurité, la supervision et l'alerting, les outils de développement et de CI/CD, ou les outils d'analytics. L'utilisation de cet outillage est lui aussi vecteur de réduction d'impact s'il ne vient pas en doublon du même outillage “on premises” car les ressources utilisées pour délivrer ces service sont mutualisées entre tous les clients et sont optimisés en termes d'intégration avec les services du CSP.

7. **Services PaaS et SaaS**

    Les services délivrés en mode PaaS et SaaS sont ceux qui permettent le meilleur niveau d'optimisation sur les vecteurs évoqués précédemment. Ils permettent donc, en théorie, d'atteindre un niveau optimal d'utilisation des équipements hardware et d'énergie pour un service rendu. Je précise bien "en théorie" car un acteur proposant un outil ayant une énorme valeur ajoutée par rapport à la concurrence pourrait se permettre de le vendre beaucoup plus cher et de ne pas se soucier de l'optimisation des ressources utilisées. Cependant, un gros acteur du SaaS aura toujours intérêt à optimiser l'utilisation des ressources matérielles et d'énergie, au moins lorsqu'il est sur un marché mature avec de la concurrence.


    Cet argument est donc moins valable pour des petits acteurs qui vendent des services SaaS reposant sur des services de cloud public, car ils ont moins de marge de manœuvre que les CSP pour optimiser et surtout parce qu'il faut avant tout qu'ils démontrent la valeur de leur outil avant d'en optimiser le coût. Les vouchers offerts par les CSP aux startups et les levées de fonds permettent généralement de se concentrer sur la valeur du produit plutôt que sur l'optimisation de l'utilisation des ressources. ;-)


     


A périmètre constant, ces avantages intrinsèques des services Cloud en font naturellement des alliés pour réduire l'impact du numérique, non seulement sur les émissions de gaz à effet de serre mais aussi sur l'épuisement de ressources abiotiques et la consommation d'énergie primaire qui sont souvent oubliées dans ce genre d'analyses.

Malgré tous ces avantages, héberger ses services dans le Cloud, peut tout de même se révéler plus impactant pour l'environnement lorsqu'on les utilise mal.

Concernant l’impact environnemental, comme pour la sécurité, les responsabilités sont partagées entre le CSP et le client : c’est au client d’utiliser convenablement les services Cloud pour réellement réduire son impact.

Voici donc quelques recommandations à suivre en tant que client pour utiliser les services Cloud de manière à réduire son impact environnemental: 



1. Privilégier les services de plus haut niveau (SaaS, PaaS) aux services d'infrastructure (IaaS) car ils permettent une mutualisation plus importante. Cela implique donc souvent de choisir un CSP parmi les plus gros du marché car les plus avancés sur ce type d'offre ou bien de choisir un acteur de niche qui se spécialise dans un type de service comme Clever Cloud ou Scalingo avec le PaaS.
2. Choisir un CSP qui pratique l'overcommit (provisioning d’une même ressource physique pour la vendre simultanément à plusieurs clients en partant du principe que les clients en question ne solliciteront pas la ressource à 100% au même moment). Le fait de ne pas faire d'overcommit était souvent vu comme un argument commercial mais j’ai bon espoir qu’il s'inverse avec de plus en plus de clients qui se soucient de l’impact environnemental.
3. Choisir le bon niveau de redondance/ disponibilité garantie en fonction des besoins réels. Idem pour les sauvegardes.
4. Eviter les effets rebond en ne cédant pas à la tentation d'utiliser toujours plus, uniquement parce que c'est facile et pas cher (en réalité c'est cher mais on s'en rend compte trop tard). Certainement la chose la plus complexe à mettre en œuvre à l'échelle d'une organisation et l'utilisation doit donc être accompagnée d'une démarche d'écoconception des services numériques pour éviter ces effets rebond.

    Il faut aussi être en capacité d'évaluer si on a réduit son impact en allant vers le Cloud et un moyen simple de le savoir, sans forcément le quantifier, est de voir si cela vous coûte moins cher chez un CSP que cela ne vous coûtait "on premises". Si c'est le cas, en restant dans le même pays, vous avez très certainement réduit votre impact car à ressource équivalente (conso elec ou matériel), les CSP sont plus chers (ceux qui ont fait des projets de lift & shift le savent) et moins impactants (pour les raisons évoquées ci-dessus).

5. Dans le cas d'une migration :
    1. il est primordial d’anticiper pour migrer à un moment où une part importante des équipements arrive en fin de vie et ainsi pouvoir décommissioner massivement des infrastructures dans un délai raisonnable
    2. éviter le "lift & shift" dans la mesure du possible
    3. réduire la durée de double run des services
6. Si la plupart des utilisateurs des services hébergés sont localisés en France, privilégier l’hébergement en France pour : 
* profiter du mix électrique faiblement carboné en France
* limiter l’impact sur le réseau
7. Eviter les patterns d'architecture avec des transferts importants de données (mais généralement cela coûte tellement cher qu'on évite naturellement, sans même se poser la question de l'impact environnemental)
8. Plus généralement, éviter d'avoir un SI hybride avec des liens forts entre le Cloud et les infrastructures "on premises". Il faudra par exemple éviter d'utiliser l'outillage existant "on premises" dans le cloud et préférer l'utilisation des services natifs. Ce choix implique un "vendor lockin" et il faudra budgéter le coût de sortie du CSP en question mais les économies réalisées vont générer tellement d'économies aux niveaux financier et environnemental que le ROI sera très rapide.

Pour conclure, je dirais qu’en théorie le Cloud est bien meilleur pour l’environnement que des infrastructures “on premises” si on l’utilise intelligemment. Toutefois, cela peut s’avérer complexe d’y migrer intelligemment lorsqu’on a déjà un gros SI hébergé “on premises”.

Malheureusement le constat actuel est que le Cloud croit sans que le nombre de Datacenters ne baisse. Cela laisse penser que la plupart des transitions vers le Cloud ne se font pas de manière optimale et qu’au lieu de réduire l’impact environnemental avec ces migrations, on l’augmente.

Le Cloud est donc : 



* à recommander sans hésitation pour les sociétés qui se lancent ainsi que pour les PME qui n’ont pas de grosses infrastructures et qui peuvent profiter de l’arrivée en fin de vie d’une partie importante de leur parc pour migrer efficacement.
* à étudier au cas par cas et certainement à préparer plusieurs années en avance pour des grosses sociétés qui disposent d’un SI “on premises” conséquent.

N’hésitez pas à commenter et à proposer des compléments, [ici](https://github.com/AirLoren/airloren.github.io/issues), sous forme d’issues sur Github, je serai ravi de les ajouter.

Limites de cet article : J’ai abordé uniquement le sujet de l'impact environnemental sur les critères d'émissions de gaz à effets de serre, consommation d'énergie primaire et épuisement de ressources abiotiques. Je n'ai pas abordé celui de l'impact social et de la souveraineté qui sont aussi des sujets à prendre en compte dans un contexte où les principaux CSP ne sont ni français ni même européens et que les pratiques de certains d'entre eux laissent à désirer en matière de fiscalité, de gestion des données personnelles et de respect du droit de la concurrence.

J’ai fait le choix de ne pas aborder le sujet des effets indirects car l’objectif de l’article est de répondre à la question initiale sans introduire trop de variables pour que les lecteurs puissent se faire un avis sur l’orientation à privilégier dans leur contexte.

Il faut cependant être conscient, à minima, des effets indirects suivants pour éviter de rendre contre productive une migration vers le Cloud :  



* les effets rebonds liés à la facilité de consommer des services Cloud
* l’impact systémique d’une concentration des hébergements dans les pays où le mix électrique est faiblement carboné (risque de saturation, surtout dans un contexte où l'électrification d’autres usages est censée contribuer à la transition énergétique)

Pour finir, il semblerait que la durée de vie des équipements utilisés par les CSP soit plus courte ([4 à 6 ans d’après les CSP](https://www.lemondeinformatique.fr/actualites/lire-apres-google-et-aws-microsoft-prolonge-la-duree-de-vie-de-ses-equipements-cloud-87581.html)) que celle des équipements utilisés “on premises” qui attendent souvent la fin de support hardware pour être décommissionnés. Cela pourrait donc atténuer les effets positifs de la mutualisation chez les CSP mais sans donnée précise, cela semble difficile d’estimer dans quelle mesure. Je reste cependant convaincu que cela ne peut pas inverser la tendance car le ratio _durée de vie CSP / durée de vie “on premises”_ reste bien supérieur au ratio _pourcentage de ressources inutilisées chez le CSP / pourcentage de ressources inutilisées “on premises”_.