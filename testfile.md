lncli listchannels | tr -d '",' |
awk '/chan_id|capacity|local_balance|remote_balance|peer_alias/{print $1 $2 $3 $4",";
if(/capacity/){ capacity = $2 } 
if(/local_balance/){ printf "%08.4f%%, \n", capacity / $2 }}' |
sed 'N;N;N;N;N;s/\n/ /g' | sort -k 4nr | awk '{print $1 $4 $6}' |
sed 's/,/", # /' | sed 's/%,/% /' |
sed 's/chan_id:/"/' | sed 's/peer_alias:/ /' | sed 's/.$//' | sed '$s/,/ /'

#[gist](https://gist.github.com/xjmzx/83fbf022c120ca0550e714978f841129)
