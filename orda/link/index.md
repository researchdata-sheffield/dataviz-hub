---
title: "Linking visualisations in ORDA to data"
---

Web-based visualisations can be included in the [visualisation showcase on ORDA][showcase] by following the instructions below.

## Prerequisites 

You will first need to prepare a small metadata visualisation.yaml file describing your visualisation. Create this via a [web form][webyaml] or [manually][yaml].

## Where data has been uploaded and published in ORDA 

1. Open ‘My data’ in your ORDA account. 
2. Select the appropriate dataset and open the ORDA record editing interface by clicking on the pencil icon to the right of the item in the ‘My data’ list.
3. In the record editing interface, drag and drop, or browse and select the YAML file and the visualisation image file, to upload them into the item record. 
4. Add ‘visualisation’ to the keyword metadata field.
5. Check the ‘Publish’ tickbox and click on ‘Save’.
6. ORDA administrators will get a notification that an edited record needs approval for publishing. ORDA administrator will check the metadata in the [visualisation.yaml][yaml] file.

## Where data has not been uploaded to ORDA, but (should be) available from another repository or website

1. Open ‘My data’ in your ORDA account. 
2. Create a new record by: 
    * Uploading the visualisation.yaml file and the visualisation image file to the ‘My data’ interface, by drag and drop or browse and select.
    * Clicking on ‘+ Create a new item’ and uploading the visualisation.yaml file and visualisation image file to the new record interface.
3. Complete the mandatory metadata fields - giving the record an appropriate title, author names, categories (subjects), keywords and description. Ensure that the word ‘visualisation’ is added to keywords.
4. Add a link (preferably a DOI) to the dataset into the ‘references’ field, where the dataset is available from an external repository.
5. Check the ‘Publish’ tickbox and click on ‘Publish item’, then ‘Yes, publish’.
6. ORDA administrators will get a notification that a new record needs approval for publishing. ORDA administrator will check the metadata in the visualisation.yaml file.
7. If the data files are not already available from a repository and issued with a DOI, you should deposit them in ORDA, by upload to the item record. This may be done after the record containing only the [visualisation.yaml][yaml] and image files has been published.

[showcase]: https://orda.shef.ac.uk/visualisations/
[webyaml]: http://vis-yaml.shef.ac.uk/
[yaml]: ../visualisation-yaml/
