# Long term notes from Omada

### future checks
- Onboarding segmentation questions:
     Brandon had this SQL command to review the dropoff of users at different pages of the onboarding process
     ``` 
     SELECT distinct a.id,
                current_disease_state,
                current_page,
                q.completed_at::date,
                a.accepted_at::date,
                CASE WHEN completed_at is null THEN FALSE ELSE TRUE END as completed_acct_setup,
                CASE WHEN (completed_at::date - accepted_at::date) > 5 OR completed_at is null then FALSE ELSE TRUE END as completed_acct_setup_within_5_days
        FROM reports_derived.accounts a
        left outer join kairos.questionnaires q on q.account_id=a.id
        where a.accepted_at BETWEEN '2022-06-01' AND '2023-12-01';
    ```