# mediawiki.aoirint.com

## Setup

```shell
# 33: www-data
sudo mkdir -p volumes/mediawiki_data volumes/mediawiki_settings volumes/mediawiki_images volumes/mediawiki_extensions
sudo chown -R 33:33 volumes/mediawiki_data volumes/mediawiki_settings volumes/mediawiki_images volumes/mediawiki_extensions
```

## Backup

```shell
sudo 7z a backups/mediawiki.aoirint.com_volumes_$(date '+%Y-%m-%d_%H-%M-%S').7z volumes/
sudo docker compose exec db mysqldump -u wikiuser -p mediawiki | sudo 7z a -si backups/mediawiki.aoirint.com_db_$(date '+%Y-%m-%d_%H-%M-%S').sql.7z

sudo chown -R root:root backups/
sudo chmod -R ga-rwx backups/
```

## Restore

```shell
sudo cat backups/mediawiki.aoirint.com_db_2022-12-06_21-31-55.sql | sudo docker compose exec -T db mysql -u wikiuser -pwikiuser_password mediawiki
```
