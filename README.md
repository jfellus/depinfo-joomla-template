# depinfo-joomla-template
Joomla Template for depinfo.u-cergy.fr


## What I changed in the source code

### /html/mod_articles_category

I modified the **mod_articles_category** module to add filtering by tag. 
For this, i modified
* helper.php :
````
          // @jfellus filter items by tag
          foreach ($items as $k => &$item)
          {
                  $taglist = '';
                  foreach($item->tags->itemTags as &$tag) $taglist .= $tag->title.' ';
                  if($params->get('tag_filter') && strpos($taglist, $params->get('tag_filter')) === false) unset($items[$k]);
          }
````

* mod_articles_category.xml : (to add a new `tag_filter` field in the module's parameters)

````
                                <field
                                        name="tag_filter"
                                        type="sql"
                                        query="SELECT id, title AS title FROM `#__tags` WHERE published=1 AND title!='ROOT'"
                                        label= "MOD_ARTICLES_TAG_TAG_LABEL"
                                        key_field="title"
                                        value_field="title"
                                        description = "MOD_ARTICLES_CATEGORY_FIELD_TAG_DESC" >
                                        multiple="false"
                                        size="5">
                                                <option value="">no filter</option>
                                </field>

````

That's all
