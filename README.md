# package com.cartoes.api.repositories;
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertTrue;
import static org.junit.Assert.fail;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.List;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.ActiveProfiles;
import org.springframework.test.context.junit4.SpringRunner;
import com.cartoes.api.entities.Transacao;
@RunWith(SpringRunner.class)
@SpringBootTest
@ActiveProfiles("test")
public class TransacaoRepositoryTest {
 @Autowired
 private TransacaoRepository transacaoRepository;

 private Transacao transacaoTeste;

 private void CriarTransacaoTestes() throws ParseException {

 transacaoTeste = new Transacao();

 transacaoTeste.setCNPJ("05887098082");
 transacaoTeste.setValor("350.00);
 transacaoTeste.setParcelas("2");
 transacaoTeste.setJuros("10.00"); 
 transacaoTeste.setDataTransacao(new
SimpleDateFormat("dd/MM/yyyy").parse("25/08/2020"));

 }

 @Before
 public void setUp() throws Exception {
	 
	 CriarTransacaoTestes();
	 transacaoRepository.save(transacaoTeste);

	 }

	 @After
	 public void tearDown() throws Exception {

	 transacaoRepository.deleteAll();

	 }

	 @Test
	 public void testFindById() {

	 Transacao transacao =
	transacaoRepository.findById(transacaoTeste.getId()).get();
	 assertEquals(transacao.getId(), transacaoTeste.getId());

	 }

	 @Test
	 public void testFindByCnpj() {

	 Transacao transacao = transacaoRepository.findByCnpj(transacaoTeste.getCnpj());
	 assertEquals(transacao.getCnpj(), transacaoTeste.getCnpj());

	 }

	 @Test
	 public void testFindByDataTransacao() {

	 List<Transacao> lstTransacao =
	transacaoRepository.findByDataTransacao(
	transacaoTeste.getDataTransacao());

	 if (lstTransacao.size() != 1) {
	 fail();
	 }

	 Transacao transacao = lstTransacao.get(0);

	transacao.getDataTransacao().equals(transacao.getDataTransacao()));

	 }
	}

 }
