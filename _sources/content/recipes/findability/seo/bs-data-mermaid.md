graph TD;
 A(HTML page):::box --> |Create markup template| B{what type <br> of resource ?}:::box
 B --> C(Chemical Substance):::box
 B --> D(Gene):::box
 B --> E(Molecular Entity):::box
 B --> F(Protein):::box
 B --> G(Sample):::box
 B --> H(Taxon):::box
 C --> I
 D --> I
 E --> I
 F --> I
 G --> I
 H --> I(Markup template):::box
 I --> |Embed template in website| J(fa:fa-search fa:fa-cog fa:fa-fighter-jet Schema.org augmented HTML page):::box
  classDef box font-family:avenir,font-size:14px,fill:#B30000,stroke:#222,color:#fff,stroke-width:1px
 linkStyle 0,1,2,3,4,5,6,7,8,9,10,11,12,13 stroke:#B30000,stroke-width:1px,color:#B30000,font-family:avenir;