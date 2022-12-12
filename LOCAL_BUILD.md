# evm_loader
1. `git clone https://github.com/neonlabsorg/neon-evm.git`
2. `cd neon-evm`
3. `git checkout v0.14.x`
4. `git submodule update --init`
5. 
```
export SOLANA_REVISION=v1.11.10
export SOLANA_IMAGE=solanalabs/solana:v1.11.10
export REVISION=v0.14.1
```

5. `docker build --build-arg SOLANA_REVISION=$SOLANA_REVISION --build-arg SOLANA_IMAGE=$SOLANA_IMAGE --build-arg REVISION=$REVISION --tag neonlabsorg/evm_loader:v0.14.1 .`

ignor erros like this
```
Error: Function _ZN8evm_core15primitive_types4U51215overflowing_pow17hb39293b73e96c896E Stack offset of 4312 exceeded max offset of 4096 by 216 bytes, please minimize large stack variables
```
# neon_test_invoke_program
1. `git clone https://github.com/neonlabsorg/neon-test-invoke-program.git`
2. `cd neon-test-invoke-program`
3. `docker build --tag neonlabsorg/neon_test_invoke_program:develop .`

# proxy

1. `git clone https://github.com/neonlabsorg/proxy-model.py.git`
2. `cd proxy-model.py`
3. 
```
export NEON_EVM_COMMIT=v0.14.1
export PROXY_REVISION=v0.14.5
export PROXY_LOG_CFG=log_cfg.json
```

4. 
```
docker build --build-arg NEON_EVM_COMMIT=$NEON_EVM_COMMIT --build-arg PROXY_REVISION=$PROXY_REVISION --build-arg PROXY_LOG_CFG=$PROXY_LOG_CFG --tag neonlabsorg/proxy:v0.14.5 .
```

# run read only proxy

```
sudo SOLANA_URL="https://api.devnet.solana.com" REVISION="v0.14.5" docker-compose -f docker-compose-operator-ro.yaml up -d
```