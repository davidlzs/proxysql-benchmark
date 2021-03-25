# DB Backend switch

This scenario tests effect of updating destination hostgroup in proxysql
query rules on in flight transactions.

The results are quite positive. It seems that proxysql does not kill
in flight transactions even if the related query rule got updated. Proxysql
will use the DB backend in the new query rule only for new transactions.

* Steps:

    - Start the docker-compose containers; 
        ```bash
        docker-compose up -d
        ```
    - Open a bash shell on the `nose` test container: ` db_backend_switch_nose_1`
        ```bash
        docker exec -it db_backend_switch_nose_1 bash
        ```
    - Run the `nose` test   
        ```bash
            cd tests
            nosetests --nocapture test_proxysql_backend_change.py
