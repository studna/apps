<template>
  <div id="explorer">
    <b-tabs v-model="activeTab">
      <b-tab-item label="Chain Info">
        <Summary />
        <!-- <b-field label="Chain">
					<b-input :value="conn.chainName" disabled></b-input>
        </b-field>
				<b-field label="Best">
					<b-input :value="nodeInfo.blockNumber" disabled></b-input>
        </b-field>
				<b-field label="Total Issuance">
					<b-input :value="nodeInfo.totalIssuance" disabled></b-input>
        </b-field>
				<b-field label="Finalized">
					<b-input :value="nodeInfo.finalized" disabled></b-input>
        </b-field>
				<b-field label="Length">
					<b-input :value="nodeInfo.session.eraLength" disabled></b-input>
        </b-field> -->
        <!-- </b-field> -->
          <!-- Chain name - {{conn.chainName}}
          last block {{nodeInfo.blockNumber}} -->
          <!-- target -> 6s -->
          <!-- total issuance {{nodeInfo.totalIssuance}} -->
          <!-- session  -->
          <!-- {{nodeInfo.session.length}} /  -->
          <!-- {{nodeInfo.sessionLength}} -->
          <!-- era {{nodeInfo.sessionsPerEra}} -->
          <!-- finalized {{nodeInfo.finalized}} -->

        <!-- [recent blocks] -->
      </b-tab-item>
      <b-tab-item label="Block Details">
				<BlockDetails :chainName="conn.chainName"
					:lastBlock="nodeInfo.blockNumber" />
      </b-tab-item>      
      <b-tab-item label="Node Info">
        <!-- <NodeDetails :totalPeers="nodeInfo.health.peers"
        :isSyncing="nodeInfo.health.isSyncing"
        :ourBest="nodeInfo.blockNumber"
         /> -->
      </b-tab-item>
    </b-tabs>
    <!-- <p>Recent Block {{conn.header.number}}</p> -->
    <!-- <p>Genesis Hash {{api.genesisHash}}</p> -->
    <!-- <p>RuntimeVersion {{api.runtimeVersion}}</p>
    <p>Library Info {{api.libraryInfo}}</p> -->

  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue, Watch } from 'vue-property-decorator';
import Router from 'vue-router';
import Card from '../shared/Card.vue';
import BlockDetails from './BlockDetails.vue';
import NodeDetails from './NodeDetails.vue';
import Summary from './Summary.vue';

@Component({
  components: {
		Card,
    BlockDetails,
    NodeDetails,
    Summary,
  },
})
export default class Explorer extends Vue {
  public activeTab: number = 0;
  public conn: any = { chain: '', nodeName: '', nodeVersion: '', header: {}};
  public bestPeer: any = null;
  public bestPeerBlock: any = null;
  public api: any = null;
  public nodeInfo: any = {
    blockNumber: '', health: '', peers: '', extrinsics: '', session: {},
    totalIssuance: '', finalized: '', era: '', sessionsPerEra: '',
  };
  private subs: any[] = [];

  // You may have an infinite update loop in watcher with expression "nodeInfo.peers"
  // @Watch('nodeInfo.peers')
  // public async sortBestPeerBlock() {
  //   // console.log(this.nodeInfo.peers.length);
  //   if (this.nodeInfo.peers.length) {
  //     this.bestPeer = this.nodeInfo.peers.sort((a: any, b: any): number => b.bestNumber.cmp(a.bestNumber))[0];
  //     this.bestPeerBlock = this.bestPeer.bestNumber;
  //   }
  // }

  // @Watch('activeTab')
  // public async updateLocation() {
  //   // console.log(typeof this.activeTab);
  //   if (typeof this.activeTab === 'number') {
  //     this.$router.replace('/explorer/' + this.activeTab);
  //   }
  // }

  public async loadExternalInfo() {
    if ((this as any).$http.api) {
      // const apiResponse = await (this as any).$http.api.rpc.system.chain();
      // this.conn.chainName = await apiResponse.toString();
      // const apiPeers = await (this as any).$http.api.rpc.system.peers();
      // this.nodeInfo.peers = await apiPeers;
      // const apiBestNumber = await (this as any).$http.api.derive.chain.bestNumber();
      // this.subs.push(await (this as any).$http.api.derive.chain.bestNumber((val: any) => {
      //   this.nodeInfo.blockNumber = val.toString();
      // }));
      // const apiHealth = await (this as any).$http.api.rpc.system.health();
      // this.nodeInfo.health = await apiHealth;

      // this.nodeInfo.blockNumber = await apiBestNumber.toString();
      // const apiSession = await (this as any).$http.api.query.session.validators();
      // this.nodeInfo.session = await apiSession;
      // const apiSessionLength = await (this as any).$http.api.query.session.sessionLength();
      // this.nodeInfo.session.length = await apiSessionLength;
      // const apiSessionProgress = await (this as any).$http.api.derive.session.sessionProgress();
      // this.nodeInfo.session.progress = await apiSessionProgress;
      // const apiSessionCurrentIndex = await (this as any).$http.api.derive.session.currentIndex;
      // this.nodeInfo.session.currentIndex = await apiSessionCurrentIndex;
      // const apiSessionEraLength = await (this as any).$http.api.derive.session.eraLength;
      // this.nodeInfo.session.eraLength = await apiSessionEraLength;
      // const apiSessionEraProgress = await (this as any).$http.api.derive.session.eraProgress;
      // this.nodeInfo.session.eraProgress = await apiSessionEraProgress;
      // const apiSessionActiveEra = await (this as any).$http.api.derive.session.activeEra;
      // this.nodeInfo.session.activeEra = await apiSessionActiveEra;
      // const apiSessionInfo = await (this as any).$http.api.derive.session.info;
      // this.nodeInfo.session.info = await apiSessionInfo;
      // const apiPendingExtrinsics = await (this as any).$http.api.rpc.author.pendingExtrinsics();
      // this.nodeInfo.extrinsics = await apiPendingExtrinsics;
      // const apiTotalIssuance = await (this as any).$http.api.query.balances.totalIssuance();
      // this.nodeInfo.totalIssuance = await apiTotalIssuance;
      // const apiFinalized = await (this as any).$http.api.derive.chain.bestNumberFinalized();
      // this.nodeInfo.finalized = await apiFinalized;

      // const apiSessionsPerEra = await (this as any).$http.api.consts.staking.sessionsPerEra();
      // this.nodeInfo.sessionsPerEra = await apiSessionsPerEra;
    }
  }

  // public async switchTab() {
  //   this.activeTab = Number(this.$route.params.tab);
  // }

  public async mounted(): Promise<void> {
    this.loadExternalInfo();
    // th is.switchTab();
  }

  public beforeDestroy() {
    this.subs.forEach((sub) => sub());
  }
}
</script>
