### List of APIs required for implementing the features

>**Note**: The mandatory APIs are required to integrate any system through SDK.

| Feature            | APIs to be Implemented                                                                                                                                                                        |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Basic Element Sync | **Element APIs:**<br>* Get<br>* Add<br>* Update<br>* Query                                                                                                                                    |
| Relation           | **Relation APIs:**<br>* Create <br>* Delete<br><br>Element Get API should also provide relations<br><br>**Element Type Get API:**<br>* Provide metadata for relations                         |
| Revisions          | **Multi Element Revision APIs:**<br>* Get revisions<br>* Get elements changed in revision <br> * Get elements at revision <br><br>**Element Type Get API:**<br>* Provide metadata for history |
