Search engine tech notes
========================

*last update: Sept. 2024*

- Backup:
    - relies on snapshot (inconsistent state - document index keeps going)
    - https://opensearch.org/docs/latest/tuning-your-cluster/availability-and-recovery/snapshots/snapshot-restore/
- Replication:
    - https://opensearch.org/blog/segment-replication/
    - In transit replication over TLS: https://opensearch.org/docs/latest/tuning-your-cluster/replication-plugin/permissions/ 
- Backpressure:
    - https://opensearch.org/docs/latest/tuning-your-cluster/availability-and-recovery/shard-indexing-backpressure/
    - https://opensearch.org/docs/latest/tuning-your-cluster/availability-and-recovery/segment-replication/backpressure/ 
- Encryption:
    - Data can be rebuilt based on the index - hence encryption required:
        - https://blog.mikemccandless.com/2010/10/lucenes-simpletext-codec.html 
        - what about ngram? 
    - Exiting community plugin - snapshot encryption for different types of repos (fs, s3, azure, gcp)
        - https://github.com/Aiven-Open/encrypted-repository-opensearch/tree/main 
        - Encryption key per repository and "client" - a string used when the snapshot repo is created
            - Per date -> snapshot
            - Per tenant -> could be mapped to the client
            - Key rotation could be done by re-encrypting the data and hence, requires the payload (see https://github.com/opensearch-project/OpenSearch/issues/3469 )
            - see https://opster.com/guides/opensearch/opensearch-operations/how-to-set-up-snapshot-repositories/
    - Product feature in progress (seems to be an endless contrib) - much better since it's not 
        - https://github.com/opensearch-project/OpenSearch/pull/12902
        - https://github.com/opensearch-project/OpenSearch/issues/3469
    - PKCS11 support:
        - not supported as of sept. 2024
        - https://github.com/opensearch-project/security/issues/3420
        - https://github.com/sternadsoftware/OpenSearch/pull/2/files
        - Support in snapshot plugun: willyborankin (owner of the encryption plugin) is following the pkcs11 implementation and will hopefully 
          support pkcs11 in the plugin: https://github.com/Aiven-Open/encrypted-repository-opensearch/blob/main/src/main/java/org/opensearch/repository/encrypted/EncryptedRepositorySettings.java
        - New plugin in progress (PR 12902 above) leverage Security provider - so PKCS11 can be used instead of SunJCE for instance - to be tested but expected to work out of the box
- Authentication
    - https://opensearch.org/docs/latest/security/authentication-backends/client-auth/#enabling-client-certificate-authentication
- Security
    - https://opensearch.org/docs/latest/security/configuration/best-practices/ 
- Lucene additional info:
    - https://lucene.apache.org/core/3_0_3/fileformats.html
    - https://j.blaszyk.me/tech-blog/exploring-apache-lucene-index/
    - https://j.blaszyk.me/tech-blog/exploring-apache-lucene-search-and-ranking/
