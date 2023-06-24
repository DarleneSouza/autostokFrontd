<template>
  <div>
    <el-table :data="tabelaData" style="width: 100%">
      <el-table-column prop="nome" label="Nome"></el-table-column>
      <el-table-column prop="obs" label="Observações"></el-table-column>
      <el-table-column prop="qtd" label="Quantidade"></el-table-column>
      <el-table-column label="Operações">
        <template slot-scope="scope">
          <el-button
            type="danger"
            icon="el-icon-delete"
            @click="excluirItem(scope.row)"
          ></el-button>
          <el-button
            type="primary"
            icon="el-icon-edit"
            @click="editarItem(scope.row)"
          ></el-button>
        </template>
      </el-table-column>
    </el-table>

    <el-dialog
      title="Confirmar Exclusão"
      :visible="exclusaoModalVisible"
      @close="exclusaoModalVisible = false"
    >
      <span>Tem certeza de que deseja excluir este item?</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="exclusaoModalVisible = false">Cancelar</el-button>
        <el-button type="danger" @click="confirmarExclusaoItem"
          >Confirmar</el-button
        >
      </span>
    </el-dialog>
    <el-dialog
      title="Adicionar Item"
      :visible="adicaoModalVisible"
      @close="adicaoModalVisible = false"
    >
      <el-form label-width="120px">
        <el-form-item label="Nome">
          <el-input v-model="novoItem.nome"></el-input>
        </el-form-item>
        <el-form-item label="Observações">
          <el-input v-model="novoItem.obs"></el-input>
        </el-form-item>
        <el-form-item label="Quantidade">
          <el-input v-model="novoItem.qtd"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="adicaoModalVisible = false">Cancelar</el-button>
        <el-button type="primary" @click="confirmarAdicaoItem"
          >Adicionar</el-button
        >
      </span>
    </el-dialog>
    <el-dialog
      title="Editar Item"
      :visible="edicaoModalVisible"
      @close="edicaoModalVisible = false"
    >
      <el-form label-width="120px">
        <el-form-item label="Nome">
          <el-input v-model="itemEdicao.nome"></el-input>
        </el-form-item>
        <el-form-item label="Observações">
          <el-input v-model="itemEdicao.obs"></el-input>
        </el-form-item>
        <el-form-item label="Quantidade">
          <el-input v-model="itemEdicao.qtd"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="edicaoModalVisible = false">Cancelar</el-button>
        <el-button type="primary" @click="confirmarEdicaoItem"
          >Confirmar</el-button
        >
      </span>
    </el-dialog>
    <el-button
      class="btn-add add"
      icon="el-icon-plus"
      @click="exibirModalAdicao"
    ></el-button>
  </div>
</template>

<script>
export default {
  name: "ListaView",
  data() {
    return {
      tabelaData: [
        { nome: "Item 1", obs: "Observação 1", qtd: 10 },
        { nome: "Item 2", obs: "Observação 2", qtd: 5 },
        { nome: "Item 3", obs: "Observação 3", qtd: 8 },
      ],
      exclusaoModalVisible: false,
      itemExclusao: null,
      adicaoModalVisible: false,
      edicaoModalVisible: false,
      novoItem: {
        nome: "",
        obs: "",
        qtd: 0,
      },
      itemEdicao: {
        nome: "",
        obs: "",
        qtd: 0,
      },
    };
  },
  methods: {
    excluirItem(item) {
      console.log("Excluir item:", item);
      this.exclusaoModalVisible = true;
    },
    confirmarExclusaoItem() {
      console.log("Excluir item:", this.itemExclusao);
      // Lógica para excluir o item da tabela
      this.exclusaoModalVisible = false;
    },
    editarItem(item) {
      console.log("Editar item:", item);
      this.itemEdicao = { ...item };
      this.edicaoModalVisible = true;
    },
    exibirModalAdicao() {
      this.novoItem = { nome: "", obs: "", qtd: 0 };
      this.adicaoModalVisible = true;
    },
    confirmarAdicaoItem() {
      // Lógica para adicionar o novo item à tabela
      this.tabelaData.push({ ...this.novoItem });
      this.adicaoModalVisible = false;
    },
    confirmarEdicaoItem() {
      // Lógica para confirmar a edição do item
      this.edicaoModalVisible = false;
    },
  },
};
</script>

<style>
.add {
  font-size: 30px;
  position: fixed;
  bottom: 10px;
  right: 10px;
  height: 70px;
  width: 70px;
  border-radius: 100px;
  border: none;
  background-color: rgb(14, 231, 14);
  color: #fff;
}
</style>
