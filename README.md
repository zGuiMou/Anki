import re

# HTML fornecido
html_content = """
<div id="materia-assuntos">
				<div id="filtro-assuntos">
					<div id="filtro-busca">
						<span id="" class="glyphicon glyphicon-search " title=""></span><input type="search" name="filtro" id="valor-busca" class="form-control" placeholder="Digite o nome ou trecho do assunto.">
					</div>
					<button type="button" id="filtrar-assuntos-button" class="roundButton btn btn-tec" title="Buscar" tabindex="">
		Buscar</button></div>

				<hr>

				<div id="header-assuntos">
					<h2 id="header-nome">Assuntos desta matéria</h2>

					<div id="header-total-questoes">questões</div>
					<div id="header-total-comentadas">comentadas</div>
					<div id="header-total-aulas">teoria</div>

					<div id="header-total-questoes-mobile"><span class="fa fa-quora"></span></div>
					<div id="header-total-comentadas-mobile"><span class="fa fa-graduation-cap"></span></div>
					<div id="header-total-aulas-mobile"><span class="fa fa-book"></span></div>
				</div>

				<div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1352">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1352" class="subassunto-nome">História do Direito do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>59</span>
        </div>

        <div class="total-comentadas">
            <span>56</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;4<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">5</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="6057">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/6057" class="subassunto-nome">Interpretação, Integração e Aplicação do Direito do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>35</span>
        </div>

        <div class="total-comentadas">
            <span>33</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;12</span>
                    <span class="visible-xs">14</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1354">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1354" class="subassunto-nome">Fontes do Direito Individual do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>151</span>
        </div>

        <div class="total-comentadas">
            <span>143</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;2<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;9</span>
                    <span class="visible-xs">12</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1353">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1353" class="subassunto-nome">Princípios do Direito Individual do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>241</span>
        </div>

        <div class="total-comentadas">
            <span>234</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;3<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">4</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1359">
				<span id="direita-1359" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1359" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1359" class="subassunto-nome">Contrato de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>4611</span>
        </div>

        <div class="total-comentadas">
            <span>4345</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;24<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;75<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;90</span>
                    <span class="visible-xs">189</span>
                </div>
    </div>
    <div id="assunto-item-filho-1359" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16597">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16597" class="subassunto-nome">Natureza Jurídica, Requisitos, Características e Sujeitos da Relação de Trabalho. Relação de Emprego.</a>
	                	</div>

        <div class="total-questoes">
             <span>739</span>
        </div>

        <div class="total-comentadas">
            <span>693</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;8<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">9</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16583">
				<span id="direita-16583" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-16583" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16583" class="subassunto-nome">Modalidades de Contrato de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>370</span>
        </div>

        <div class="total-comentadas">
            <span>352</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;4<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;7<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">11</span>
                </div>
    </div>
    <div id="assunto-item-filho-16583" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16584">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16584" class="subassunto-nome">Contrato por Tempo Indeterminado</a>
	                	</div>

        <div class="total-questoes">
             <span>26</span>
        </div>

        <div class="total-comentadas">
            <span>24</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16585">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16585" class="subassunto-nome">Contrato por Tempo Determinado</a>
	                	</div>

        <div class="total-questoes">
             <span>128</span>
        </div>

        <div class="total-comentadas">
            <span>120</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;2<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">3</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16586">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16586" class="subassunto-nome">Contrato de Experiência</a>
	                	</div>

        <div class="total-questoes">
             <span>66</span>
        </div>

        <div class="total-comentadas">
            <span>61</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16587">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16587" class="subassunto-nome">Contrato Intermitente</a>
	                	</div>

        <div class="total-questoes">
             <span>34</span>
        </div>

        <div class="total-comentadas">
            <span>34</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1369">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1369" class="subassunto-nome">Trabalho Temporário (Lei nº 6.019/1974)</a>
	                	</div>

        <div class="total-questoes">
             <span>116</span>
        </div>

        <div class="total-comentadas">
            <span>113</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;3<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">4</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1363">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1363" class="subassunto-nome">Suspensão e Interrupção (Contrato de Trabalho)</a>
	                	</div>

        <div class="total-questoes">
             <span>508</span>
        </div>

        <div class="total-comentadas">
            <span>482</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1362">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1362" class="subassunto-nome">Alteração (Contrato de Trabalho)</a>
	                	</div>

        <div class="total-questoes">
             <span>291</span>
        </div>

        <div class="total-comentadas">
            <span>274</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;3</span>
                    <span class="visible-xs">5</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1364">
				<span id="direita-1364" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1364" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1364" class="subassunto-nome">Contratos Especiais de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>733</span>
        </div>

        <div class="total-comentadas">
            <span>693</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;12<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;49<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;30</span>
                    <span class="visible-xs">91</span>
                </div>
    </div>
    <div id="assunto-item-filho-1364" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1365">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1365" class="subassunto-nome">Emprego Doméstico (LC nº 150/2015)</a>
	                	</div>

        <div class="total-questoes">
             <span>119</span>
        </div>

        <div class="total-comentadas">
            <span>107</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;6<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;17</span>
                    <span class="visible-xs">24</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1366">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1366" class="subassunto-nome">Aprendizagem (CLT, Lei nº 10.097/2000 e Decreto nº 9.579/2018)</a>
	                	</div>

        <div class="total-questoes">
             <span>155</span>
        </div>

        <div class="total-comentadas">
            <span>149</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;7</span>
                    <span class="visible-xs">8</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1367">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1367" class="subassunto-nome">Estágio (Lei nº 11.788/2008)</a>
	                	</div>

        <div class="total-questoes">
             <span>164</span>
        </div>

        <div class="total-comentadas">
            <span>156</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;6</span>
                    <span class="visible-xs">7</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1368">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1368" class="subassunto-nome">Trabalho Avulso (Lei nº 12.815/2013 e Lei nº 12.023/2009)</a>
	                	</div>

        <div class="total-questoes">
             <span>79</span>
        </div>

        <div class="total-comentadas">
            <span>76</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;10<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">11</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1370">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1370" class="subassunto-nome">Trabalho Rural (Lei nº 5.889/1973)</a>
	                	</div>

        <div class="total-questoes">
             <span>81</span>
        </div>

        <div class="total-comentadas">
            <span>79</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1371">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1371" class="subassunto-nome">Professores (arts. 317 a 323 da CLT)</a>
	                	</div>

        <div class="total-questoes">
             <span>9</span>
        </div>

        <div class="total-comentadas">
            <span>9</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1374">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1374" class="subassunto-nome">Desporto Profissional (Lei nº 9.615/1998)</a>
	                	</div>

        <div class="total-questoes">
             <span>26</span>
        </div>

        <div class="total-comentadas">
            <span>20</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;12<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">13</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1375">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1375" class="subassunto-nome">Aeronautas (Lei nº 13.475/2017)</a>
	                	</div>

        <div class="total-questoes">
             <span>10</span>
        </div>

        <div class="total-comentadas">
            <span>10</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;13<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">14</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1378">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1378" class="subassunto-nome">Jornalistas (arts. 302 a 316 da CLT)</a>
	                	</div>

        <div class="total-questoes">
             <span>8</span>
        </div>

        <div class="total-comentadas">
            <span>7</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="10231">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/10231" class="subassunto-nome">Químicos (arts. 325 a 350 da CLT)</a>
	                	</div>

        <div class="total-questoes">
             <span>52</span>
        </div>

        <div class="total-comentadas">
            <span>51</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1380">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1380" class="subassunto-nome">Mãe Social e Mãe Crecheira (Lei nº 7.644/1987)</a>
	                	</div>

        <div class="total-questoes">
             <span>13</span>
        </div>

        <div class="total-comentadas">
            <span>13</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="6060">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/6060" class="subassunto-nome">Trabalhador Autônomo</a>
	                	</div>

        <div class="total-questoes">
             <span>13</span>
        </div>

        <div class="total-comentadas">
            <span>12</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;2<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">3</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="9529">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/9529" class="subassunto-nome">Atividades de Exploração, Perfuração, Produção e Refinação de Petróleo, Industrialização do Xisto, Indústria Petroquímica e Transporte de Petróleo e seus Derivados por Dutos (Lei nº 5.811/1972)</a>
	                	</div>

        <div class="total-questoes">
             <span>4</span>
        </div>

        <div class="total-comentadas">
            <span>4</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1391">
				<span id="direita-1391" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1391" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1391" class="subassunto-nome">Extinção do Contrato de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>1927</span>
        </div>

        <div class="total-comentadas">
            <span>1809</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;5<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;8<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;57</span>
                    <span class="visible-xs">70</span>
                </div>
    </div>
    <div id="assunto-item-filho-1391" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1392">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1392" class="subassunto-nome">Formas de Ruptura do Contrato de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>467</span>
        </div>

        <div class="total-comentadas">
            <span>435</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;2<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">3</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1393">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1393" class="subassunto-nome">Justa Causa</a>
	                	</div>

        <div class="total-questoes">
             <span>335</span>
        </div>

        <div class="total-comentadas">
            <span>309</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;15</span>
                    <span class="visible-xs">16</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1394">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1394" class="subassunto-nome">Aviso Prévio</a>
	                	</div>

        <div class="total-questoes">
             <span>362</span>
        </div>

        <div class="total-comentadas">
            <span>343</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;11</span>
                    <span class="visible-xs">12</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1395">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1395" class="subassunto-nome">Garantias Provisórias de Emprego</a>
	                	</div>

        <div class="total-questoes">
             <span>377</span>
        </div>

        <div class="total-comentadas">
            <span>361</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;6<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;22</span>
                    <span class="visible-xs">29</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1396">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1396" class="subassunto-nome">FGTS (Fundo de Garantia do Tempo de Serviço)</a>
	                	</div>

        <div class="total-questoes">
             <span>386</span>
        </div>

        <div class="total-comentadas">
            <span>361</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;9</span>
                    <span class="visible-xs">10</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16599">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16599" class="subassunto-nome">Contrato Nulo, Trabalho Ilícito e Trabalho Proibido</a>
	                	</div>

        <div class="total-questoes">
             <span>28</span>
        </div>

        <div class="total-comentadas">
            <span>27</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;1<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16598">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16598" class="subassunto-nome">Inexistência de Vínculo (Cooperativas, Entidades Religiosas, Trabalho Voluntário, Empreitada, etc)</a>
	                	</div>

        <div class="total-questoes">
             <span>15</span>
        </div>

        <div class="total-comentadas">
            <span>15</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1381">
				<span id="direita-1381" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1381" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1381" class="subassunto-nome">Remuneração</a>
	                	</div>

        <div class="total-questoes">
             <span>1501</span>
        </div>

        <div class="total-comentadas">
            <span>1392</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;7<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;23</span>
                    <span class="visible-xs">30</span>
                </div>
    </div>
    <div id="assunto-item-filho-1381" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1382">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1382" class="subassunto-nome">Salário e Remuneração</a>
	                	</div>

        <div class="total-questoes">
             <span>175</span>
        </div>

        <div class="total-comentadas">
            <span>160</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;1</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="2309">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/2309" class="subassunto-nome">Salário Utilidade ou Salário in Natura</a>
	                	</div>

        <div class="total-questoes">
             <span>161</span>
        </div>

        <div class="total-comentadas">
            <span>151</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1400">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1400" class="subassunto-nome">Adicionais de Insalubridade e Periculosidade</a>
	                	</div>

        <div class="total-questoes">
             <span>414</span>
        </div>

        <div class="total-comentadas">
            <span>396</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;6</span>
                    <span class="visible-xs">7</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="2308">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/2308" class="subassunto-nome">Gratificação Natalina (13º Salário)</a>
	                	</div>

        <div class="total-questoes">
             <span>85</span>
        </div>

        <div class="total-comentadas">
            <span>76</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="2310">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/2310" class="subassunto-nome">Gorjetas e Demais Componentes</a>
	                	</div>

        <div class="total-questoes">
             <span>289</span>
        </div>

        <div class="total-comentadas">
            <span>262</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1383">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1383" class="subassunto-nome">Regras de Proteção do Salário</a>
	                	</div>

        <div class="total-questoes">
             <span>169</span>
        </div>

        <div class="total-comentadas">
            <span>153</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;7</span>
                    <span class="visible-xs">8</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1385">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1385" class="subassunto-nome">Equiparação Salarial</a>
	                	</div>

        <div class="total-questoes">
             <span>199</span>
        </div>

        <div class="total-comentadas">
            <span>185</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;9</span>
                    <span class="visible-xs">10</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16600">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16600" class="subassunto-nome">Direitos Intelectuais sobre o Trabalho do Empregado</a>
	                	</div>

        <div class="total-questoes">
             <span>9</span>
        </div>

        <div class="total-comentadas">
            <span>9</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1386">
				<span id="direita-1386" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1386" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1386" class="subassunto-nome">Duração do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>2359</span>
        </div>

        <div class="total-comentadas">
            <span>2209</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;6<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;29</span>
                    <span class="visible-xs">35</span>
                </div>
    </div>
    <div id="assunto-item-filho-1386" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1387">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1387" class="subassunto-nome">Jornada de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>759</span>
        </div>

        <div class="total-comentadas">
            <span>709</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="6062">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/6062" class="subassunto-nome">Horas Suplementares</a>
	                	</div>

        <div class="total-questoes">
             <span>214</span>
        </div>

        <div class="total-comentadas">
            <span>188</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1388">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1388" class="subassunto-nome">Intervalos (Trabalho)</a>
	                	</div>

        <div class="total-questoes">
             <span>272</span>
        </div>

        <div class="total-comentadas">
            <span>258</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;5</span>
                    <span class="visible-xs">6</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1389">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1389" class="subassunto-nome">Repouso Semanal Remunerado</a>
	                	</div>

        <div class="total-questoes">
             <span>79</span>
        </div>

        <div class="total-comentadas">
            <span>74</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;6</span>
                    <span class="visible-xs">7</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1390">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1390" class="subassunto-nome">Férias (Trabalho)</a>
	                	</div>

        <div class="total-questoes">
             <span>833</span>
        </div>

        <div class="total-comentadas">
            <span>796</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;14</span>
                    <span class="visible-xs">15</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1971">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1971" class="subassunto-nome">Trabalho Noturno</a>
	                	</div>

        <div class="total-questoes">
             <span>202</span>
        </div>

        <div class="total-comentadas">
            <span>184</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;4</span>
                    <span class="visible-xs">5</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16476">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16476" class="subassunto-nome">Teletrabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>110</span>
        </div>

        <div class="total-comentadas">
            <span>110</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1397">
				<span id="direita-1397" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1397" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1397" class="subassunto-nome">Tutelas Especiais (Trabalho)</a>
	                	</div>

        <div class="total-questoes">
             <span>492</span>
        </div>

        <div class="total-comentadas">
            <span>462</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;2<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;11</span>
                    <span class="visible-xs">13</span>
                </div>
    </div>
    <div id="assunto-item-filho-1397" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1398">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1398" class="subassunto-nome">Proteção do Trabalho do Menor (Trabalho Infantil)</a>
	                	</div>

        <div class="total-questoes">
             <span>207</span>
        </div>

        <div class="total-comentadas">
            <span>192</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1399">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1399" class="subassunto-nome">Proteção do Trabalho da Mulher</a>
	                	</div>

        <div class="total-questoes">
             <span>285</span>
        </div>

        <div class="total-comentadas">
            <span>270</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;11</span>
                    <span class="visible-xs">12</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="5176">
				<span id="direita-5176" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-5176" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/5176" class="subassunto-nome">Acidente de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>147</span>
        </div>

        <div class="total-comentadas">
            <span>134</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div id="assunto-item-filho-5176" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16551">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16551" class="subassunto-nome">Definição de Acidente de Trabalho, Abrangência, Equiparação</a>
	                	</div>

        <div class="total-questoes">
             <span>79</span>
        </div>

        <div class="total-comentadas">
            <span>71</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16552">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16552" class="subassunto-nome">Direitos do Empregado em Caso de Acidente (Estabilidade, Afastamento Remunerado, etc)</a>
	                	</div>

        <div class="total-questoes">
             <span>28</span>
        </div>

        <div class="total-comentadas">
            <span>26</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16553">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16553" class="subassunto-nome">Responsabilidades e Obrigações do Empregador em Caso de Acidente de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>40</span>
        </div>

        <div class="total-comentadas">
            <span>37</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1925">
				<span id="direita-1925" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1925" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1925" class="subassunto-nome">Responsabilidade Trabalhista</a>
	                	</div>

        <div class="total-questoes">
             <span>394</span>
        </div>

        <div class="total-comentadas">
            <span>369</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;3<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;13</span>
                    <span class="visible-xs">16</span>
                </div>
    </div>
    <div id="assunto-item-filho-1925" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1926">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1926" class="subassunto-nome">Grupo Econômico (Responsabilidade Trabalhista)</a>
	                	</div>

        <div class="total-questoes">
             <span>126</span>
        </div>

        <div class="total-comentadas">
            <span>113</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1927">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1927" class="subassunto-nome">Sucessão Trabalhista</a>
	                	</div>

        <div class="total-questoes">
             <span>120</span>
        </div>

        <div class="total-comentadas">
            <span>117</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;8</span>
                    <span class="visible-xs">9</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1928">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1928" class="subassunto-nome">Terceirização (Responsabilidade Trabalhista)</a>
	                	</div>

        <div class="total-questoes">
             <span>148</span>
        </div>

        <div class="total-comentadas">
            <span>139</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;5</span>
                    <span class="visible-xs">6</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1929">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1929" class="subassunto-nome">Prescrição e Decadência (Direito do Trabalho)</a>
	                	</div>

        <div class="total-questoes">
             <span>178</span>
        </div>

        <div class="total-comentadas">
            <span>171</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1401">
				<span id="direita-1401" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1401" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1401" class="subassunto-nome">Direito Coletivo do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>1182</span>
        </div>

        <div class="total-comentadas">
            <span>1067</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;7<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;23</span>
                    <span class="visible-xs">30</span>
                </div>
    </div>
    <div id="assunto-item-filho-1401" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1402">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1402" class="subassunto-nome">Princípios do Direito Coletivo do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>64</span>
        </div>

        <div class="total-comentadas">
            <span>60</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;7</span>
                    <span class="visible-xs">8</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1403">
				<span id="direita-1403" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-1403" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1403" class="subassunto-nome">Sujeitos Coletivos do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>411</span>
        </div>

        <div class="total-comentadas">
            <span>349</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;3<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;7</span>
                    <span class="visible-xs">10</span>
                </div>
    </div>
    <div id="assunto-item-filho-1403" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1404">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1404" class="subassunto-nome">Espécies. Sindicatos. Federações. Confederações</a>
	                	</div>

        <div class="total-questoes">
             <span>341</span>
        </div>

        <div class="total-comentadas">
            <span>283</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1405">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1405" class="subassunto-nome">Constituição e Registro</a>
	                	</div>

        <div class="total-questoes">
             <span>22</span>
        </div>

        <div class="total-comentadas">
            <span>21</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1406">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1406" class="subassunto-nome">Fontes de Receita</a>
	                	</div>

        <div class="total-questoes">
             <span>48</span>
        </div>

        <div class="total-comentadas">
            <span>45</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;7</span>
                    <span class="visible-xs">8</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1407">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1407" class="subassunto-nome">Negociação Coletiva (Convenções)</a>
	                	</div>

        <div class="total-questoes">
             <span>401</span>
        </div>

        <div class="total-comentadas">
            <span>372</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="1412">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/1412" class="subassunto-nome">Greve</a>
	                	</div>

        <div class="total-questoes">
             <span>230</span>
        </div>

        <div class="total-comentadas">
            <span>214</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;9</span>
                    <span class="visible-xs">10</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="4247">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/4247" class="subassunto-nome">Comissões de Conciliação Prévia Trabalhista (CCPT)</a>
	                	</div>

        <div class="total-questoes">
             <span>76</span>
        </div>

        <div class="total-comentadas">
            <span>72</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="4652">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/4652" class="subassunto-nome">Direito Administrativo do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>100</span>
        </div>

        <div class="total-comentadas">
            <span>88</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;16</span>
                    <span class="visible-xs">17</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="4697">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/4697" class="subassunto-nome">Direito Internacional do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>128</span>
        </div>

        <div class="total-comentadas">
            <span>123</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;18</span>
                    <span class="visible-xs">19</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="2826">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/2826" class="subassunto-nome">Dano Extrapatrimonial (Material, Moral, Assédio)</a>
	                	</div>

        <div class="total-questoes">
             <span>77</span>
        </div>

        <div class="total-comentadas">
            <span>73</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">1</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="6059">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/6059" class="subassunto-nome">Métodos de Resolução de Conflito</a>
	                	</div>

        <div class="total-questoes">
             <span>32</span>
        </div>

        <div class="total-comentadas">
            <span>30</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;6</span>
                    <span class="visible-xs">7</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16236">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16236" class="subassunto-nome">Sistema de Dados Trabalhistas (RAIS, CAGED etc.)</a>
	                	</div>

        <div class="total-questoes">
             <span>31</span>
        </div>

        <div class="total-comentadas">
            <span>20</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="2831">
				<span id="direita-2831" class="glyphicon glyphicon-triangle-right triangulo-oculto" title=""></span><span id="baixo-2831" class="glyphicon glyphicon-triangle-bottom assunto-triangulo" title=""></span></span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/2831" class="subassunto-nome">Jurisprudência dos Tribunais Superiores em Matéria Trabalhista </a>
	                	</div>

        <div class="total-questoes">
             <span>1171</span>
        </div>

        <div class="total-comentadas">
            <span>1135</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;61</span>
                    <span class="visible-xs">61</span>
                </div>
    </div>
    <div id="assunto-item-filho-2831" class="assunto-filho">
            <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14401">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14401" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Princípios do Direito Individual do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>11</span>
        </div>

        <div class="total-comentadas">
            <span>11</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14402">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14402" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Direitos Constitucionais Trabalhistas</a>
	                	</div>

        <div class="total-questoes">
             <span>2</span>
        </div>

        <div class="total-comentadas">
            <span>2</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14403">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14403" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Fontes do Direito Individual do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>4</span>
        </div>

        <div class="total-comentadas">
            <span>4</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14404">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14404" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Relação de Trabalho e Relação de Emprego</a>
	                	</div>

        <div class="total-questoes">
             <span>31</span>
        </div>

        <div class="total-comentadas">
            <span>30</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14405">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14405" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Carteira de Trabalho e Previdência Social (CPTS)</a>
	                	</div>

        <div class="total-questoes">
             <span>3</span>
        </div>

        <div class="total-comentadas">
            <span>2</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14406">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14406" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Contrato de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>86</span>
        </div>

        <div class="total-comentadas">
            <span>83</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14407">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14407" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Contratos Especiais de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>23</span>
        </div>

        <div class="total-comentadas">
            <span>22</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;4</span>
                    <span class="visible-xs">4</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14408">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14408" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Remuneração</a>
	                	</div>

        <div class="total-questoes">
             <span>223</span>
        </div>

        <div class="total-comentadas">
            <span>215</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;17</span>
                    <span class="visible-xs">17</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14409">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14409" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Duração do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>177</span>
        </div>

        <div class="total-comentadas">
            <span>174</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14410">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14410" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Extinção do Contrato de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>283</span>
        </div>

        <div class="total-comentadas">
            <span>278</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;10</span>
                    <span class="visible-xs">10</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14411">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14411" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Tutelas Especiais Trabalhistas</a>
	                	</div>

        <div class="total-questoes">
             <span>13</span>
        </div>

        <div class="total-comentadas">
            <span>13</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;6</span>
                    <span class="visible-xs">6</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14412">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14412" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Acidente de Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>7</span>
        </div>

        <div class="total-comentadas">
            <span>7</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;2</span>
                    <span class="visible-xs">2</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14413">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14413" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Responsabilidade Trabalhista</a>
	                	</div>

        <div class="total-questoes">
             <span>122</span>
        </div>

        <div class="total-comentadas">
            <span>116</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;4</span>
                    <span class="visible-xs">4</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14414">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14414" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Prescrição e Decadência</a>
	                	</div>

        <div class="total-questoes">
             <span>38</span>
        </div>

        <div class="total-comentadas">
            <span>37</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14415">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14415" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Direito Coletivo do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>99</span>
        </div>

        <div class="total-comentadas">
            <span>95</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;18</span>
                    <span class="visible-xs">18</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14416">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14416" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Dano Extrapatrimonial (Material, Moral, Assédio)</a>
	                	</div>

        <div class="total-questoes">
             <span>10</span>
        </div>

        <div class="total-comentadas">
            <span>10</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="14417">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/14417" class="subassunto-nome">Jurisprudência dos Tribunais Superiores sobre Assuntos Diversos e/ou Outros Assuntos Trabalhistas</a>
	                	</div>

        <div class="total-questoes">
             <span>39</span>
        </div>

        <div class="total-comentadas">
            <span>36</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="6013">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/6013" class="subassunto-nome">CTPS - Carteira de Trabalho e Previdência Social</a>
	                	</div>

        <div class="total-questoes">
             <span>232</span>
        </div>

        <div class="total-comentadas">
            <span>218</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;6</span>
                    <span class="visible-xs">7</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="6058">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/6058" class="subassunto-nome">Direitos Constitucionais Trabalhistas</a>
	                	</div>

        <div class="total-questoes">
             <span>184</span>
        </div>

        <div class="total-comentadas">
            <span>177</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;1<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;15</span>
                    <span class="visible-xs">16</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="16594">
				<span class="icone-bola">.</span>
					</span>
          <a href="https://www.tecconcursos.com.br/aulas/materias/10/assuntos/16594" class="subassunto-nome">Outros Temas e Questões Mescladas de Direito do Trabalho</a>
	                	</div>

        <div class="total-questoes">
             <span>114</span>
        </div>

        <div class="total-comentadas">
            <span>110</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    <div class="subassunto">
        <div class="subassunto-titulo">
            <span class="icone-arvore expandir" id="">
				<span class="icone-bola">.</span>
					</span>
          <span class="subassunto-nome">Sem Classificação de Assunto</span>
                </div>

        <div class="total-questoes">
             <span>475</span>
        </div>

        <div class="total-comentadas">
            <span>1</span>
        </div>

        <div class="total-aulas">
            <span class="hidden-xs">
                        <i class="fa fa-book" title="Texto" tec-tooltip=""></i>&nbsp;0<i class="fa fa-video-camera" title="Vídeo" tec-tooltip=""></i>&nbsp;0<i class="fa fa-sitemap" title="Mapa Mental" tec-tooltip=""></i>&nbsp;0</span>
                    <span class="visible-xs">0</span>
                </div>
    </div>
    </div>
"""

# Usando expressão regular para encontrar todos os tópicos e subtópicos
pattern = r'<a href="[^"]+" class="subassunto-nome">([^<]+)</a>'
topicos = re.findall(pattern, html_content)

# Exibindo os tópicos encontrados
for i, topico in enumerate(topicos, 1):
    print(f"{i}. {topico}")
