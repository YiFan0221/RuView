# RuView 部署進度（YF）

更新：2026-05-28

## ESP32-S3 燒錄完成（4 張）

| 板子 | MAC | TDM Slot | IP（DHCP） |
|------|-----|----------|------------|
| 第 1 張 | e0:72:a1:ce:7d:38 | slot 0/4 | 192.168.2.109 |
| 第 2 張 | e0:72:a1:ce:ee:90 | slot 1/4 | 192.168.2.110 |
| 第 3 張 | 14:c1:9f:2a:16:d4 | slot 2/4 | 192.168.2.111 |
| 第 4 張 | 14:c1:9f:2a:0c:40 | slot 3/4 | 192.168.2.113 |

- Firmware: v0.6.6，release_bins/s3-adr110/
- Flash 位址：bootloader@0x0，partition-table@0x8000，ota_data@0xf000，app@0x20000
- WiFi SSID 和 target-ip 已寫入 NVS（不記錄於此）

## 遠端主機（spaceGEN3-WIFI）

- SSH: `ssh adminpc@192.168.2.112`（見 ~/.ssh/config: Host spaceGEN3-WIFI）
- OS: Ubuntu 24.04，Rust 1.95.0（~/.cargo/bin/cargo）
- docker-compose 1.29.2
- Repo: ~/Documents/RuView

## 下一步（依序）

1. `cd ~/Documents/RuView && git pull`（遠端缺少 homecore-* crates）
2. `docker build -f docker/Dockerfile.homecore -t ruview-homecore:latest .`
3. `docker run -d --name homecore -p 8123:8123 ruview-homecore:latest`
4. 確認 homecore-server 在 8123 回應，ESP32 CSI 資料進來

## 已知問題

- `sensing-server` Docker build 失敗：hnsw_rs workspace 編譯問題（E0658），暫時繞過
- `wifi-densepose-desktop` 需要 GTK/JavaScriptCoreGTK，headless server 測試需加 `--exclude wifi-densepose-desktop`
- Dockerfile.homecore 已建立並 scp 至遠端（docker/Dockerfile.homecore）
