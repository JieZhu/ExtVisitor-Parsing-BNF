package model;

import java.io.FileNotFoundException;
import java.util.Set;

import extvisitor.IExtVisitorCmd;

import parser.*;
import token.Token;
import token.tokenizer.*;


/**
 * Factory with methods to create various parsing visitor factories for various predtermined grammars
 * @author swong
 *
 */
public class ParserFactFactory {
	/**
	 * Singleton instance
	 */
	public static final ParserFactFactory Singleton = new ParserFactFactory();
	private ParserFactFactory() {
	}

	/**
	 * Make original grammar parser.
	 *  
	 *  E ::= F E1
	 *  F ::= F1 | F2
	 *  F1 ::= NumToken
	 *  F2 ::= IdToken
	 *  E1 ::= E1a | Empty
	 *  E1a ::= + E
	 * 
	 */
	public ITokVisitorFact makeOrigParser(String filename, ITokenizer tkzr) {

		ProxyFact eFact_Proxy = new ProxyFact(); // use this wherever E appears in the grammar, except the very beginning.

		ITokVisitorFact eFact = new SequenceFact("E", tkzr,
				new CombinationFact("F", tkzr, 
						new TerminalSymbolFact("Num", tkzr), 
						new TerminalSymbolFact("Id", tkzr)),
						new CombinationFact("E1", tkzr, 
								new SequenceFact("E1a", tkzr, 
										new TerminalSymbolFact("+", tkzr), 
										eFact_Proxy), 
										new MTSymbolFact(tkzr)));

		eFact_Proxy.setFact(eFact);  // close the loop


		System.err.println("Parser Factory = " + eFact);

		return eFact;
	}


	/**
	 * Make simple XML parser.
	 *
	 * TaggedElt ::= < Id > AXML </ Id > 
	 * AXML  ::=  NEXML | Empty   
	 * NEXML ::=  AElement AXML 
	 * AElement ::=  Id | TaggedElt 
	 * 
	 * Notes:
	 * "</" is a single token above, not two tokens
	 * 
	 * @param filename The input file to parse
	 * @return a factory for making the parsing visitor
	 */
	public ITokVisitorFact makeXMLParser(String filename, ITokenizer tkzr) {

		ITokVisitorFact leftBracketFact = new TerminalSymbolFact("<", tkzr);
		ITokVisitorFact rightBracketFact = new TerminalSymbolFact(">", tkzr);
		//    ITokVisitorFact forwardSlashFact = new TerminalSymbolFact("\"/\"", tok);
		ITokVisitorFact idFact = new TerminalSymbolFact("Id", tkzr);
		ITokVisitorFact leftBracketForwardSlashFact = new TerminalSymbolFact("</", tkzr);

		ProxyFact taggedElt_Proxy = new ProxyFact();

		ProxyFact aXML_Proxy = new ProxyFact();

		ITokVisitorFact aXML = new CombinationFact("AXML", tkzr,
				new MultiSequenceFact("NEXML", tkzr,
						new CombinationFact("AElement", tkzr,
								idFact, taggedElt_Proxy),
								aXML_Proxy), 
								new MTSymbolFact(tkzr));
		aXML_Proxy.setFact(aXML);

		ITokVisitorFact taggedElt = new MultiSequenceFact("EFac", tkzr,
				leftBracketFact, idFact, rightBracketFact,
				aXML, 
				leftBracketForwardSlashFact, idFact, rightBracketFact);

		taggedElt_Proxy.setFact(taggedElt);

		System.err.println("Parser Factory = " + taggedElt);

		return taggedElt;
	}

	
	/**
	 * Make a parser for BNF
	 * BNF of BNF
	 * 
	 * S   ::= D | S1
	 * S1  ::= "\n" S
	 * D   ::=  Id "::=" E L
	 * 
	 * L   ::=  L2 | Empty
	 * L2  ::=  "\n"  L3
	 * L3  ::=  L | D
	 * 
	 * E   ::=  T E1
	 * E1  ::=  Empty | E1a
	 * E1a ::=  "|" E
	 * 
	 * T   ::= T1 T2
	 * T1  ::= Id| QuotedStringToken
	 * T2  ::= Empty | T
	 * 
	 * @param filename The file to read in
	 * @return a factory to make a parsing visitor
	 * @throws FileNotFoundException
	 */
	public ITokVisitorFact makeBNFParser(String filename, ITokenizer tkzr, final Set<String> keywordSet) {

// Alternate code for decorating the tokenizer rather than decorating the TerminalSymbolFact:
	  
//  public ITokVisitorFact makeBNFParser(String filename, final ITokenizer tkzr0, final Set<String> keywordSet) {
//
//    // Decorate the tokenizer to find the keywords,
//    // which are all the QuotedStringTokens in the BNF input
//    ITokenizer tkzr = new ITokenizer() {
//      @Override public Token getNextToken() {
//        Token t = tkzr0.getNextToken();
//        if (t.getName().equals("QuotedStringToken")) keywordSet.add(t.getLexeme());
//        return t;
//      }
//      @Override public void putBack(Token t) { tkzr0.putBack(t); }
//    };
	  
		// STUDENT TO COMPLETE
	
	
		return new MTSymbolFact(tkzr);  // STUDENT REPLACE RETURN VALUE!
	}


}
