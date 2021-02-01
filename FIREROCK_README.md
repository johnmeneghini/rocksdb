# NetApp Firerock Development Branch 

This is the main NetApp SPDK/rocks-db development branch for Firerock.

  - All modifications made to rocks-db by NetApp should be made in a sub-branch off of this branch.
  - All modifcations made to the rocks-db code will be BSD licensed, open source software
  - Modifications made to this branch may be donated back to the SPDK project.
  - Modifications made to this branch are subject to the NetApp OSRB code review process.

Contact: johnm@netapp.com for more information.

# KV-Store Repository Setup 

The new Bitbucket KV-STORE project is located at: https://bitbucket.eng.netapp.com/projects/KV-STORE-BB

Use the new setup-kv-store.sh setup script to set up a local working repository: `/x/eng/site/smokejumper/spdk/autotest/setup-kv-store.sh`

This script replaces the setup-spdk.sh script.

# Building SPDK and RocksDB

From the spdk dir:
```
   ./configure
   make -j $(nproc)
```

You can build rocksdb with:
```
   env USE_RTTI=1 make db_bench DEBUG_LEVEL=0 EXTRA_CXXFLAGS='-Wno-deprecated-copy -Wno-pessimizing-move -Wno-error=stringop-truncation' SPDK_DIR=<path to spdk> -j $(nproc)
```
Use the SPDK script to setup vfio for the NVME card.
```
   sudo env NRHUGE=6144 scripts/setup.sh
```

run perf tests with the SPDK script
```
   sudo env USE_RTTI=1 test/blobfs/rocksdb/rocksdb.sh
```

NOTE: Make sure you have /usr/bin and /usr/local/bin ahead of /usr/software/bin in $PATH or you will have an unpleasant experience!  

How to release SPDK claimed devices back to kernel:
```
   sudo scripts/setup.sh reset
```
