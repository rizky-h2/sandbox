# NOTES

## About Store Code

- Store code is the store's unique ID
  - It has specific format defined from the store data stored in Kintone (e.g. me9999902)
- There are **two tables** that hold store code data
  - `users`: `id`
    - for stores registered and displayed on GMAC
  - `business_profile_locations`: `store_code`, `store_code_labels`
    - for stores registered on GBP account
    - normally, store code can be retrieved from `store_code` column. However, in case store code is changed, the new store code is stored on `store_code_labels`
    - By default, `store_code_labels` has the same value with `store_code`
- Linking stores on GMAC with the data from GBP
  - store with `users.id` = `business_profile_locations.store_code_labels` is linked together
    - Everytime there are updates on GBP, data for the same store on GMAC will also be updated
    - Data sync on GMAC is done by executing `php artisan batches:fetch_update_gbp_locations` (this batch program is executed automatically once everyday)
  - There may be multiple account data on GMAC for one store, however, the one that is updated is the one that fulfil `users.id` = `business_profile_locations.store_code_labels`

## Notes on business_profile_locations

TBD
