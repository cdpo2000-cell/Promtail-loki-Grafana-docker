# snort3-Promtail-loki-Grafana-docker
sudo apt-get update //更新套件清單

sudo apt-get install -y apt-transport-https software-properties-common wget //安裝必要的套件

sudo mkdir -p /etc/apt/keyrings //建立key的目錄

wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null //下載並加入 Grafana GPG 金鑰

echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list  //加入來源

sudo apt-get update //更新套件清單

sudo apt-get install promtail //安裝promtail

sudo usermod -aG adm promtail //將adm使用者加入到該群組中

sudo mkdir -p /var/lib/promtail //建立目錄

sudo groupadd promtail //建立promtail群組

sudo usermod -aG promtail promtail //將promtail使用者加入到該群組中

sudo chown -R promtail:promtail /var/lib/promtail //修改目錄所有權

sudo chmod 755 /var/lib/promtail //確保權限正確

sudo systemctl start promtail //啟動Promtail

sudo systemctl enable promtail //設定開機自動啟動

sudo systemctl status promtail //檢查狀態顯示 active (running)就成功了

sudo -u promtail ls -l /var/log/snort/alert_json.txt //檢查檔案是否可讀

sudo chmod 644 /var/log/snort/alert_json.txt //修改權限

sudo chmod 755 /var/log/snort/  //修改權限

journalctl -u promtail -f //追蹤日誌觀察

/etc/promtail/config.yml  
